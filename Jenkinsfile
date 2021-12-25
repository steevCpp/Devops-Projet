
pipeline {
    agent any
    
   environment {
     imageName = 'steevdev7/my-private-ripo'

    registryCredentialSet = 'dockerhub'

  }

 stages {
      stage('clone') {
           steps {
             
                git branch: 'master', url: 'https://github.com/steevCpp/Devops-Projet/'
             
          }
        }
 
   //stage('Génère war Maven') {
    //      steps {
             
   //             sh 'mvn package'             
  //        }
   //     }


   stage('Docker Build compose') {
           steps {
              
                sh 'mkdir sessions data/mysq logs/mysql ' 

                sh 'docker-compose build ' 

          }
        }


      stage('envoie image  sur dockerhub') {
             
            steps {
                sh "docker commit contenairDevops steevdev7/my-private-ripo"
                
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u steevdev7 --password-stdin'

                sh "docker push steevdev7/my-private-ripo:latest"
                
                sh'docker logout'
                 
           

       }
 }
     
 }
}
