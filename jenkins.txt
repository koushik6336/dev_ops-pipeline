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
                bat 'mvn clean package'
            }
        }

        stage('Verify Build') {
            steps {
                echo 'Checking if JAR is created...'
                bat 'dir target'
            }
        }
    }
}