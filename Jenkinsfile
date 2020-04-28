pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '--expose 3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
      }
    }

  }
  environment {
    VIRTUAL_HOST = 'creating-a-pipeline-in-blue-ocean.pipeline.ninepla.net'
  }
}