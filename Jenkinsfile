
pipeline {
    agent any 
    stages {
        stage('CONTAINERS') {
            steps {
                script {
                    def containers = sh(script: 'docker container ls', returnStdout: true).trim()
                    echo "Containers: ${containers}"
                }
            }
        }
        stage('BUILD') {
            steps {
                script {
                    def buildOutput = sh(script: 'docker build -t ecomm .', returnStdout: true).trim()
                    echo "Build Output: ${buildOutput}"
                }
            }
        }
        stage('DEPLOY') {
            steps {
                script {
                    // Stop and remove any existing container with the name ecomm-con
                    sh '''
                        if [ "$(docker ps -a -q -f name=ecomm-con)" ]; then
                            docker stop ecomm-con || true
                            docker rm ecomm-con || true
                        fi
                    '''
                    // Run the new container
                    def runOutput = sh(script: 'docker container run -dt --name ecomm-con -p 60:80 ecomm', returnStdout: true).trim()
                    echo "Run Output: ${runOutput}"
                }
            }
        }
    }
}
