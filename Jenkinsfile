@Library('Cohort2_SharedLibrary')_
pipeline{
  agent any
  environment {
    DEPLOY_ENV = 'staging'
    GIT_REPO_URL = 'https://github.com/Gensogram-Inc/maven-web-app.git'
  }
  tools {
    maven 'maven3.9.7'
  }
  stages {
    stage('Clone from Github'){
      steps{
        git "${GIT_REPO_URL}"
      }
    }
    stage('Build with Maven'){
      steps{
        common("Build")
      }
    }
    stage('Test with Sonar'){
      steps{
        common("Test")
      }
    }
    stage('Deployment stage'){
      steps{
        script {
          if (env.DEPLOY_ENV == 'staging'){
          deploy adapters: [
            tomcat9(
                credentialsId: 'Tomcat_Cred',
                path:         '',
                url:          'http://35.183.34.87:7000/'
            )
            ],
            contextPath: null,
            war:         'target/*.war'
          }
          else if (env.DEPLOY_ENV == 'production'){
            echo 'Deploying to production tomcat'
          }
        }
      }
    }
  }
}
