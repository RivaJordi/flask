pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(url: 'https://github.com/RivaJordi/flask', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t rivajordi/flask_app .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'docker login -u rivajordi -p dckr_pat_45KcZzjCLAUlwFjNWX0IsxxArck'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker push rivajordi/flask_app'
      }
    }

  }
}