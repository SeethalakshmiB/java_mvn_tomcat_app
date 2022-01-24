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

        // stage('Deploy into docker host') {
        //     steps {
        //     //     echo "Deploying application into docker host instance"
        //         sshagent( credentials: ['docker_host'] ) {
        //             sh '''
        //                 ssh  -o StrictHostKeyChecking=no ec2-user@ec2-3-93-234-80.compute-1.amazonaws.com uptime
        //                 ssh -t ec2-user@ec2-3-93-234-80.compute-1.amazonaws.com "ls -lh; cat /etc/hostname; sudo docker run -dp 8080:8080 seetha123/pac_tomcat"
        //             '''
        //         }
        //     }
        // }
    }
}

// 1. dev --> v1 release push --> jenkins 
//     a. mvn package 
//     b. custom image and run the container -- v1

// 2. dev_1 --> v2 
//     a. mvn package
//     b. custom image --> remove previous container (v1) --> run new container (v2)

