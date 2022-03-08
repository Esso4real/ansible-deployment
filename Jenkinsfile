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
                      //sh "scp -o StrictHostKeyChecking=no ansible/* eawangya@${ANSIBLE_SERVER}:/home/eawangya/Desktop"
                        sh "ssh -o StrictHostKeyChecking=no eawangya@${ANSIBLE_SERVER}"
                      withCredentials([sshUserPrivateKey(credentialsId: 'aws-ec2sever-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                       sh 'scp $keyfile eawangya@$ANSIBLE_SERVER:/home/eawangya/Desktop/ssh-key.pem'
                    } 
               }
           }
       }
   }             
    }    
 
    }
