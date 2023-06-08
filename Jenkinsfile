pipeline {
   agent {
      docker {image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.socket:/var/run/docker.socket'
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
         environment{
               SONAR_URL="http://localhost:9000"
            }
         steps{
            sh 'echo ignore this step'
}
         }
      }
   }
   post {
        always {
            cleanWs()
        }
}
