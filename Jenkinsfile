pipeline {
  agent any
  stages {
    
    stage('Cleanup') { // Cleanup
      steps {
        step[$class: 'WsCleanup']
      }
    }

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
          sudo scp -i /home/ec2-user/hemant_kamat.pem -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/20934-jenkins ec2-user@ec2-54-167-215-55.compute-1.amazonaws.com:~
          sudo chmod 400 /home/ec2-user/hemant_kamat.pem
          echo "done"
          sudo ssh -i /home/ec2-user/hemant_kamat.pem ec2-54-167-215-55.compute-1.amazonaws.com
          PATH=$WORKSPACE/venv/bin:/usr/local/bin:$PATH
          python3 -m venv myvenv
          source myvenv/bin/activate
          pip install -r requirements.txt
          ./myvenv/bin/python3 hello.py
          

          """
        }
      }
   }
  

  }
}
