//Scripted
/* node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Test"
	}
} */

// Declarative
pipeline {
  agent any
  // agent { docker { image 'maven:3.8.7' } }
  // agent { docker { image 'node:19.4' } }
  environment {
    dockerHome = tool 'myDocker'
    mavenHome = tool 'myMaven'
    PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
  }
  stages {
    stage('Checkout') {
      steps {
        sh 'mvn --version'
        // sh 'node --version'
        sh 'docker version'
        echo "Checkout"
        echo "PATH - $PATH"
        echo "BUILD NUMBER - $env.BUILD_NUMBER"
        echo "BUILD ID - $env.BUILD_ID"
        echo "BUILD JOB NAME - $env.JOB_NAME"
        echo "BUILD TAG - $env.BUILD_TAG"
        echo "BUILD URL - $env.BUILD_URL"
      }
    }
    stage('Compile') {
      steps {
        echo "Compile"
        sh 'mvn clean compile'
      }
    }
    stage('Test') {
      steps {
        echo "Test"
        sh 'mvn test'
      }
    }
    stage('Integration Test') {
      steps {
        echo "Integration Test"
        sh 'mvn failsafe:integration-test failsafe:verify'
      }
    }
    stage('Package') {
      steps {
        echo "Package"
        sh 'mvn package -DskipTests'
      }
    }
    stage('Build Docker Image') {
      steps {
        // "docker build -t iamapsrajput/currency-exchange-devops:$env.BUILD_TAG"
        script {
          dockerImage = docker.build("iamapsrajput/currency-exchange-devops:${env.BUILD_TAG}")
        }
      }
    }
    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry('', 'dockerhub') {
            dockerImage.push();
            dockerImage.push('latest');
          }
        }
      }
    }
  }

  post {
    always {
      echo "I am awesome. I run always"
    }
    success {
      echo "I run when you are successful"
    }
    failure {
      echo "I run when you fail."
    }
  }
}