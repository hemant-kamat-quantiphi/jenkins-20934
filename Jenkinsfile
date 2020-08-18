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
        sh 'PATH=$WORKSPACE/venv/bin:/usr/local/bin:$PATH && python3 -m venv myvenv && source myvenv/bin/activate && pip install -r requirements.txt '
      }
    }

    stage('Linting') { // Run pylint against your code
     steps {
        script {
         sh """
          ./myvenv/bin/pylint test.py
          """
        }
      }
   }

    stage('test') {
      steps {
        sh './myvenv/bin/python3 -m unittest'
      }
    }

  stage('Deploy') { // Run pylint against your code
     steps {
        script {
         sh """
          sudo scp -i /home/ec2-user/hemant_kamat.pem -o StrictHostKeyChecking=no -r /home/ec2-user/ ec2-3-95-208-69.compute-1.amazonaws.com:~
          """
        }
      }
   }
  

  }
}
