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
         environment{
            DOCKER_IMAGE = "ci-cd-jenkins-sonar-argocd-k8s:${BUILD_NUMBER}"
            REGISTRY_CREDENTIALS = credentials('docker-cred')
         }
         steps{
            sh'docker build -t ${DOCKER_IMAGE} .'
         }
      }
      }
   
   }
