pipeline {
    agent any

    environment {
        ANSIBLE_SERVER = "18.218.171.120"
    }
    stages {  
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/Esso4real/ansible-deployment.git'
            }
        }       
       stage("copy files to ansible server") {
           steps {
               script{
                   echo "copying files to ansible control node"
                   sshagent(['ansible-server-key']) {
                      sh "scp -o StrictHostKeyChecking=no ansible/* ec2-user@${ANSIBLE_SERVER}:/"

                      withCredentials([sshUserPrivateKey(credentialsId: 'ansible-sever-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                       sh 'scp $keyfile ec2-user@$ANSIBLE_SERVER:/ssh-key.pem'
                        } 
                    }
                }
            }
        }  
    } 
}