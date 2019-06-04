pipeline {
  agent {
    node {
      label 'my-node-proxy'
    }

  }
  stages {
    stage('error') {
      steps {
        sh 'echo "hello world"'
      }
    }
  }
}