
pipeline {
   agent { label: 'kslave1' }
    stages {
       stage('Checkout'){
          steps {
             checkout scm 
               }
           }
     stage('puppet install'){
          steps {
            sh ' ansible-playbook -i hosts.yml puppet-playbook.yml' 
               }
         }
    stage('Docker install'){
          steps {
            sh 'ansible-playbook -i hosts.yml docker-playbook.yml' 
               }
           }
    
    stage('php Container Deploy-Testserver'){
          steps {
            sh  'ansible-playbook -i hosts.yml finalproject1-playbook.yml'
                 }
          }
      stage('php Container Deploy-Prodserver'){
          steps {
 //     ansible-playbook -i host.yml finalproject1-playbook.yml
        println "Prod Deploy Successfull"
             }
         }
    }
post {
   failure {
      echo 'Deleting running container'
     sh '''
        sudo docker rm -f $(ps -aq)
       '''
}
}
}

