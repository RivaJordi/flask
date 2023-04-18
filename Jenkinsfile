pipeline {
    environment {
        registry = 'rivajordi/flask_app'
        registryCredentials = 'docker'
        cluster_name = 'skillstorm'
        namespace = 'rivajordi'
    }
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
<<<<<<< HEAD
        git(url: 'https://github.com/rivajordi/flasky', branch: 'main')
=======
        git(url: 'https://github.com/rivajordi/flasky', branch: 'main')
>>>>>>> 6e8bbb2968aa4511b9dcc93abcf3f66871495e6f
      }
    }
stage('Build Stage') {
    steps {
        script {
            dockerImage = docker.build(registry)
        }
      }
    }
stage('Deploy Stage') {
    steps {
        script {
           docker.withRegistry('', registryCredentials) {
                dockerImage.push()
            }
          }
        }
      }
stage('Kubernetes') {
  steps {
    withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS_SECRET_ACCESS_KEY']) {
      sh "aws eks update-kubeconfig --region -us-east-1 --name ${cluster_name}"
      script{
        try{
          sh "kubectl create namespace ${namespace}"
          }catch (Exception e) {
              echo "Exception handled"
          }
          }
        sh "kubectl apply -f deployment.yaml -n ${namespace}"
        sh "kubbectl -n ${namespace} rollout restart deployment flaskcontainer"
        }
      }
    }
  }  
}