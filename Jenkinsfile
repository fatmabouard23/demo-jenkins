pipeline {
  agent {
    docker {
      image 'node:20-alpine'
      args '-e npm_config_cache=/tmp/.npm'
    }
  }
  environment {
    NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    NETLIFY_SITE_ID    = credentials('netlify-site-id')
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
    stage('Install CLI') {
      steps {
        sh 'npm install netlify-cli'
        sh 'npx netlify --version'
      }
    }
    stage('Deploy') {
      steps {
        sh 'npx netlify deploy --dir=build --prod'
      }
    }
  }
  post {
    always {
      junit 'junit.xml'
    }
  }
}
