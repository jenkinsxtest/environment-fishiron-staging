pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "jenkins-x-staging"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'sleep 300'
            sh 'HTTPS_PROXY=http://arxan:arxan@qy.arxan.proxy.wl166.com:21 helm repo add storage.googleapis.com https://storage.googleapis.com/chartmuseum.jenkins-x.io ;jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'http://arxan:arxan@qy.arxan.proxy.wl166.com:21 helm repo add storage.googleapis.com https://storage.googleapis.com/chartmuseum.jenkins-x.io ;jx step helm apply'
          }
        }
      }
    }
  }
}
