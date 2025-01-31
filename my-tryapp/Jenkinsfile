pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dhairyajadav/my-tryapp'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/DHAIRYANJADAV/tryapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dhairyajadav/my-tryapp:latest .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker login -u dhairyajadav -p DhairyaDocker@123'
                    sh 'docker push dhairyajadav/my-tryapp:latest'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    sh """
                    ssh -i "C:\Users\91942\Downloads\try-key.pem" ec2-user@ec2-13-127-36-6.ap-south-1.compute.amazonaws.com'
                    docker pull dhairyajadav/my-tryapp:latest &&
                    docker run -d -p 3000:3000 my-tryapp dhairyajadav/my-tryapp:latest

                    '
                    """
                }
            }
        }
    }
}
