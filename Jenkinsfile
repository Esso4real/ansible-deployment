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
                      sh "scp -o StrictHostKeyChecking=no ansible/* eawangya@${ANSIBLE_SERVER}:/home/eawangya"

                      withCredentials([sshUserPrivateKey(credentialsId: '', keyFileVariable: 'keyfail', usernameVariable: 'user')])
                       sh 'scp $keyfile eawangya@$ANSIBLE_SERVER:/home/eawangya/Desktop/ssh-key.pem'
                    } 
               }
           }
       }

       //trigger ansible
       }             
        
    }
