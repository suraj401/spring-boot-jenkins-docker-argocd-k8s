pipeline{
   agent any
 stages{
  stage("Code checkout"){
      steps{
      checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Supriyo-Roy/ci-cd-spring-boot-jenkins-docker-argocd-k8s.git']])
   sh 'ls -l'
   }
   }
}
}