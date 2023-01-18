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
  stages {
    stage('Build') {
      steps {
				//sh 'mvn --version'
				// sh 'node --version'
        echo "Build"
				echo "PATH - $PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "BUILD JOB NAME - $env.JOB_NAME"
				echo "BUILD TAG - $env.BUILD_TAG"
				echo "BUILD URL - $env.BUILD_URL"
      }
    }
    stage('Test') {
      steps {
        echo "Test"
      }
    }
    stage('Integration Test') {
      steps {
        echo "Integration Test"
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