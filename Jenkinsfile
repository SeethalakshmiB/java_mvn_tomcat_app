pipeline {
    agent any

    stages {
        stage('Build Maven Project') {
            steps {
                echo 'Maven Build Processing..'
                sh('/opt/apache-maven-3.8.4/bin/mvn clean')
                sh('/opt/apache-maven-3.8.4/bin/mvn package')
            }
        }
        stage('Testing Application') {
            steps {
                echo 'Skipping Test Phase..'
            }
        }
        stage('Build Docker Image and Deploy in same host') {
            steps {
                echo 'Build Docker Image....'
                sh('docker ps')
                sh('docker build -t tomcat_app .')
                sh('docker rm -f tomcat_app && echo "Removed Previous docker container successfully" || echo "No previous build"')
                sh('docker run --name tomcat_app -dp 3000:8080 tomcat_app')
            }
        }

        // stage('Ansible Playbook') {
        //     steps{
        //         sh'''
        //         echo "Ansible Stage"
        //         ansible-playbook playbook.yaml
        //         '''
        //     }
        // }
    }
}
