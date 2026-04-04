pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                echo 'Building project...'
                bat 'mvnw.cmd clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t devops-pipeline:v1 .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                echo 'Listing Docker images...'
                bat 'docker images'
            }
        }

        stage('Deploy Container') {
            steps {
                echo 'Deploying container...'
                bat '''
                echo Stopping old container...
                docker stop devops-container || exit 0

                echo Removing old container...
                docker rm devops-container || exit 0

                echo Running new container...
                docker run -d -p 8082:8082 --name devops-container devops-pipeline:v1
                '''
            }
        }
    }
}