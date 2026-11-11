pipeline {
  agent {
    docker {
      image 'node:20-alpine'
      args '-e npm_config_cache=/tmp/.npm'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
  }
  post {
    always {
      junit 'junit.xml'
    }
  }
}
