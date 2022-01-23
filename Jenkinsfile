pipeline {
    agent any

    stages {
        stage('Build Maven Project') {
            steps {
                echo 'Building..'
                sh('mvn clean')
                sh('mvn package')
            }
        }
        stage('Test') {
            steps {
                echo 'Skipping Test Phase..'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Build Docker Image....'
                sh('docker ps')
                sh('docker build -t tomcat_app .')
                sh('docker rm -f tomcat_app && echo "Removed Previous docker container successfully" || echo "No previous build"')
                sh('docker run --name tomcat_app -dp 3000:8080 tomcat_app')
            }
        }

        stage('Deploy into docker host') {
            steps {
                echo "Deploying application into docker host instance"
                sshagent( credentials: ['docker_host'] ) {
                    sh '''
                        docker ps
                    '''
                }
            }
        }
    }
}