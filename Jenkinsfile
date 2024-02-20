pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: '', branch: ''
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        docker build -t andrewyss/cicdtest:green .
        docker push andrewyss/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment myweb --image=andrewyss/cicdtest:green
        kubectl expose deployment myweb --type=LoadBalancer --port=80 --target-port=80 --name=svc_myweb
        '''
      }
    }
  }
}

  
