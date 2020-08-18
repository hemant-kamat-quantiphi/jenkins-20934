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
        sh 'PATH=$WORKSPACE/venv/bin:/usr/local/bin:$PATH && python3 -m venv myvenv && source myvenv/bin/activate && pip install -r requirements.txt --download-cache=/tmp/$JOB_NAME '
      }
    }

  //  stage('Linting') { // Run pylint against your code
   //  steps {
      //  script {
    //     sh """
       //   pylint --h
      //    """
      //  }
     // }
   // }

    stage('test') {
      steps {
        sh 'python3 -m unittest'
      }
    }

  }
}
