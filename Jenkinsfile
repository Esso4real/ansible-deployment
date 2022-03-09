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
                   sshagent([ec2-server-key']) {
                      //sh "scp -o StrictHostKeyChecking=no ansible/* ec2-user@${ANSIBLE_SERVER}:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@${ANSIBLE_SERVER}"
                      withCredentials([sshUserPrivateKey(credentialsId: 'ec2-sever-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                       sh 'scp $keyfile ec2-user@$ANSIBLE_SERVER:/home/ec2-user/ssh-key.pem'
                    } 
               }
           }
       }
   }             
    }    
 
    }
