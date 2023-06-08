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
            sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=happy \\
  -Dsonar.projectName=\'Happy\' \\
  -Dsonar.host.url=http://127.0.0.1:9000 \\
  -Dsonar.token=sqp_e5857ddd8f4926e13123edd5a17a1cc068920ca1'''
}
         }
      }
   }
   post {
        always {
            cleanWs()
        }
}
}