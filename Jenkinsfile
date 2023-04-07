pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
      git branch: 'main', url: 'https://github.com/Imlucky883/jenkins-sonar-argo-k8s'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Static Code Analysis') {
      environment {
        SONAR_URL = "http://3.81.26.185:9000"
      }
      steps {
        withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
        }
      }
    }
}
}
