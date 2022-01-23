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
                sh('docker build -t tomcat_app')
                sh('docker run -dp 8081:8080 tomcat_app')
            }
        }
    }
}