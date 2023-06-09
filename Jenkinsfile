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
      stage('Build and Push Docker Image') {
      environment {
        DOCKER_IMAGE = "supriyohub/ci-cd-jenkins-docker-argocd-k8s:${BUILD_NUMBER}"
        // DOCKERFILE_LOCATION = "java-maven-sonar-argocd-helm-k8s/spring-boot-app/Dockerfile"
        REGISTRY_CREDENTIALS = credentials('docker-creds')
      }
      steps {
        script {
            sh 'docker build -t ${DOCKER_IMAGE} .'
            def dockerImage = docker.image("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', "docker-creds") {
                dockerImage.push()
            }
        }
      }
    }
    stage('Update Deployment file'){
      environment{
         GIT_REPO_NAME = "ci-cd-spring-boot-jenkins-docker-argocd-k8s"
         GIT_USER_NAME = "Supriyo-Roy"
      }
      steps{
         withCredentials([string(credentialsId: 'Supriyo-Roy', variable: 'git-token')]) {
         sh '''
              git config user.email "roysupriyoroy@gmail.com"
                    git config user.name "Supriyo Roy"
                    BUILD_NUMBER=${BUILD_NUMBER}
                    ls -lrth
                    cd argo-config
                    sed -i "s/tagname/${BUILD_NUMBER}/g" deployment.yml
                    git add argo-config/deployment.yml
                    git commit -m "Update deployment image to version ${BUILD_NUMBER}"
                    git push https://${git-token}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                '''
}

      }
    }
      }}
