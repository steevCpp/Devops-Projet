
pipeline {
    agent any
    
  //options{
     // buildDiscader(logRotator(numToKeepStr: '5'))
 // }
     tools
    {
       maven "Maven"
    } 
   environment {
    DOCKERHUB_CREDENTIALS=credentials('dockerhub')
  }

 stages {
      stage('clone') {
           steps {
             
                git branch: 'master', url: 'https://github.com/steevCpp/Tp-Devops.git'
             
          }
        }
 
   stage('Génère war Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }

   stage('Docker Build') {
           steps {
              

                sh 'docker build -t imagedevops:latest .' 

          }
        }
        stage('Run Docker container on Jenkins') {
             
            steps {
                
                sh "docker run -d -p 8083:8080 --name contenairDevops imagedevops:latest"
 
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
