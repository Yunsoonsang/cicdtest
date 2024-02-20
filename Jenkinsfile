pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/Yunsoonsang/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t andrewyss/cicdtest:green .
        sudo docker push andrewyss/cicdtest:green
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb --image=andrewyss/cicdtest:green'
        ansible master -m command -a 'kubectl expose deploy myweb --type=LoadBalancer --port=80 --target-port=80'
        '''
      }
    }
  }
}
