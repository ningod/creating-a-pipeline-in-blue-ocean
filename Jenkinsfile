pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '--expose 3000 -e PIPELINE_NETWORK --network $PIPELINE_NETWORK -e VIRTUALHOST creating-a-pipeline-in-blue-ocean.$PIPELINE_NETWORK '
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
}