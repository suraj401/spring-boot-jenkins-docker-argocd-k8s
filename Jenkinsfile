pipeline {
   agent {
      docker {image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
      }
         }
   stages{
      stage('Code Checkout from GIT'){
         steps{
            sh 'pwd'
            sh 'ls -lrth'
         }
      }
      stage('Code Build & Test using MAven'){
         steps{
            sh 'mvn clean package'
         }
      }
      stage('Analyzing the code with SONARQUBE'){
            steps{
            sh 'echo ignore this step'
            }
         }
      stage('Build Docker Image and Push'){
            steps{
            sh'docker build -t ${DOCKER_IMAGE} .'
         }
      }
      stage('Push imge to docker hub'){
         steps{
               withCredentials([string(credentialsId: 'Docker-pwd', variable: 'docker-cred')]) {
                  sh'docker login -u supriyohub -p ${docker-cred}'
                  sh'docker push supriyohub/${DOCKER_IMAGE}'
               }
         }
      }
      }
   
   }
