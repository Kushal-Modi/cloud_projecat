pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Get the latest code from GitHub
                git branch: 'main', url: 'https://github.com/Kushal-Modi/cloud_projact.git'
            }
        }

        stage('Build - Java') {
            steps {
                // Example for a Maven project
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Build - Node.js') {
            steps {
                // Example for Node.js project
                sh 'npm install'
            }
        }

        stage('Test - Java') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Test - Node.js') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                // Build a Docker image
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                // Push Docker image to DockerHub (replace with your repo)
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker tag myapp:latest my-dockerhub-user/myapp:latest'
                    sh 'docker push my-dockerhub-user/myapp:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Example: deploy using Docker Compose
                sh 'docker-compose up -d'
            }
        }
    }
}
