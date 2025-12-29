pipeline {
  agent any

  tools {
    maven 'maven-3'
  }

  environment {
    APP_NAME = "devsecops-demo"
    IMAGE_TAG = "1.0.${BUILD_NUMBER}"
    OTEL_SERVICE_NAME = "jenkins-devsecops-demo"
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/arumbunitha/devsecops-demo-app.git'
      }
    }

    stage('Build') {
      steps {
        sh '/opt/homebrew/bin/mvn -version'
        sh '/opt/homebrew/bin/mvn clean package'
      }
    }
/*
    stage('SAST - Dependency Scan') {
      steps {
        dependencyCheck(
          odcInstallation: 'DC',
          additionalArguments: '--scan . --disableAssembly'
    )
      }
    }
*/
    stage('Docker Build') {
      steps {
        sh "docker build -t ${APP_NAME}:${IMAGE_TAG} ."
      }
    }

    stage('Image Scan') {
      steps {
        sh "trivy image ${APP_NAME}:${IMAGE_TAG}"
      }
    }

    stage('Deploy (Mock)') {
      steps {
        sh 'echo Deploying application (mock stage)'
      }
    }
  }

  post {
    success {
      echo "Pipeline succeeded"
    }
    failure {
      echo "Pipeline failed"
    }
  }
}

