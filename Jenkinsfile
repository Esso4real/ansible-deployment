pipeline {
    agent any

    environment {
        ANSIBLE_SERVER = "18.188.199.93"
    }
    stages {     
       stage("copy files to ansible server") {
           steps {
               script{
                   echo "copying files to ansible control node"
                   sshagent(['ec2-server-key']) {
                      sh "scp -o StrictHostKeyChecking=no ansible/* ec2-user@${ANSIBLE_SERVER}:/home/ec2-user"
                       
                      withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                       sh 'scp $keyfile ec2-user@$ANSIBLE_SERVER:/home/ec2-user/ssh-key.pem'
                         } 
                       }
                    }
                }
            }
        stage("Execute ansible playbook on target server"){
            steps{
                script {
                    echo "Calling playbook to configure target environment"
                    //need to install another plugin which will ebables us to exec cmdline cmds on remote servers
                    //install ssh pipeline steps plugin
                         def remote = [:]
                         remote.name = "ansible-server"
                         remote.host = "${ANSIBLE_SERVER}"
                         remote.allowAnyHosts = true

                         withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                         remote.user = user
                         remote.identityFile = keyfile
                         sshCommand remote: remote, command: "ansible-playbook playbook.yaml"  
                         }
                         

                }
            }
        }                 
        }          
    }
