pipeline {
agent any 
stages {
    stage('CONTAINERS') {
        steps {
           sh 'docker container ls'
      }
    }
    stage('BUILD') {
        steps {
           sh 'docker build -t ecomm .'
      }
    }
    stage('DEPLOY') {
        steps {
           sh 'docker container run -dt --name ecomm-con -p 60:80 ecomm'
      }
    }
  }
}
