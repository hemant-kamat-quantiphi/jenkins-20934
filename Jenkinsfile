pipeline {
  agent any
  stages {

    stage('Checkout') { // Checkout (git clone ...) the projects repository
      steps {
        checkout scm
      }
    }

    stage('build') {
      steps {
        sh 'python3 -m venv myvenv && source myvenv/bin/activate && pip install -r requirements.txt'
      }
    }

    stage('Linting') { // Run pylint against your code
      steps {
        script {
          sh """
          pylint *.py
          """
        }
      }
    }

    stage('test') {
      steps {
        sh 'python3 -m unittest'
      }
    }

  }
}
