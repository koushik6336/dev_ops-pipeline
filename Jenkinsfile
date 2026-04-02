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
    }
}