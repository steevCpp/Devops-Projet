
pipeline {
    agent any
    
   environment {
    DOCKERHUB_CREDENTIALS=credentials('dockerhub')
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
              

                sh 'docker-compose build .' 

          }
        }


      stage('envoie sur dockerhub') {
             
            steps {
                sh "docker commit contenairDevops steevdev7/my-private-ripo"
                
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u steevdev7 --password-stdin'

                sh "docker push steevdev7/my-private-ripo:latest"
                
                sh'docker logout'
                 
           

       }
 }
     
 }
}
