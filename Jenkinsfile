pipeline {
    agent any 
    stages {
        stage('WORKDIR') {
            steps {
                script {
                    def workdir = sh(script: 'pwd', returnStdout: true).trim()
                    echo "Working Directory: ${workdir}"
                }
            }
        }
        stage('BUILD') {
            steps {
                script {
                    def buildOutput = sh(script: 'docker build -t login .', returnStdout: true).trim()
                    echo "Build Output: ${buildOutput}"
                }
            }
        }
        stage('DEPLOY') {
            steps {
                script {
                    // Check for and remove any existing container with the same name
                    def existingContainer = sh(script: 'docker ps -a -q -f name=login-con', returnStdout: true).trim()
                    if (existingContainer) {
                        echo "Existing container found: ${existingContainer}"
                        sh 'docker stop login-con || true'
                        sh 'docker rm login-con || true'
                    } else {
                        echo "No existing container named login-con"
                    }

                    // Run the new container
                    try {
                        def runOutput = sh(script: 'docker container run -dt --name login-con -p 70:80 login', returnStdout: true).trim()
                        echo "Run Output: ${runOutput}"
                    } catch (Exception e) {
                        echo "Error running container: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to run container")
                    }
                }
            }
        }
    }
}
