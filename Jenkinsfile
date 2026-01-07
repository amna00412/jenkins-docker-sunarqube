pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                // Ye stage GitHub se code uthayegi
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // SonarQube scan ka kaam yahan hoga
                echo "Running SonarQube Scan..."
            }
        }

        stage('Build Docker Image') {
            steps {
                // Docker image banane ki command
                sh "docker build -t my-app-image ."
            }
        }

        stage('Deploy to Docker Server') {
            steps {
                // Ye stage code ko Docker server par deploy karegi
                echo "Deploying to Docker Server at 13.49.245.34"
            }
        }
    }
}
