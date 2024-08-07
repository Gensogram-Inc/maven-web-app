pipeline {
  agent any
  tools {
    maven 'maven3.9.6'
  }
  stages{
    stage('Clone from GitHub') {
      steps{
        echo 'Cloning from GitHub'
        git 'https://github.com/Gensogram-Inc/maven-web-app.git'
        echo 'Cloning done'
      }
    }
    stage('Testing with SonarQube') {
      steps{
        echo 'Testing with SonarQube'
        sh 'mvn sonar:sonar'
        echo 'Testing done'
      }
    }
    stage('Build with Maven') {
      steps{
        echo 'Building with Maven'
        sh 'mvn package'
        echo 'Building done'
      }
    }
    stage('Deploy to Nexus') {
      steps{
        echo 'Deploying to Nexus'
        sh 'mvn deploy'
        echo 'Deployed to Nexus'
      }
    }
    stage('Deploy to Tomcat') {
      steps{
        echo 'Deploying to Tomcat'
        deploy adapters: [tomcat9(credentialsId: 'Tomcat_Cred', path: '', url: 'http://3.99.143.117:8080/')], contextPath: null, war: 'target/*war'
        echo 'Successfully Deployed'
      }
    }
  }
  post {
    always {
      echo "Pipeline/Build Done"
    }
    success {
      echo "Build Successful"
    }
    failure {
      echo "Build failed"
    }
  }
}
