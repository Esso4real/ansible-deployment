pipeline {
    agent any

    environment {
        ANSIBLE_SERVER = "10.0.0.195"
    }
    stages {         
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