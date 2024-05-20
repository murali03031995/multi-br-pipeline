pipeline {
agent any 
stages {
    stage('WORKDIR') {
        steps {
           sh 'pwd'
      }
    }
    stage('BUILD') {
        steps {
           sh 'docker build -t login .'
      }
    }
    stage('DEPLOY') {
        steps {
           sh 'docker container run -dt --name login-con -p 70:80 login'
      }
    }
  }
}
