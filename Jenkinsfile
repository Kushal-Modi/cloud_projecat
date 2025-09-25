pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Get the latest code from GitHub
                git branch: 'main', url: 'https://github.com/Kushal-Modi/cloud_projecat.git'
            }
        }

        stage('Build - Java') {
            steps {
                // Maven build (skip tests)
                bat 'mvn clean install -DskipTests'
            }
        }

        stage('Build - Node.js') {
            steps {
                // Node.js install
                bat 'npm install'
            }
        }

        stage('Test - Java') {
            steps {
                // Run Java tests
                bat 'mvn test'
            }
        }

        stage('Test - Node.js') {
            steps {
                // Run Node.js tests
                bat 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                // Build Docker image
                bat 'docker build -t myapp:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                // Push Docker image to DockerHub
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                    bat 'docker tag myapp:latest my-dockerhub-user/myapp:latest'
                    bat 'docker push my-dockerhub-user/myapp:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy using Docker Compose
                bat 'docker-compose up -d'
            }
        }
    }
}
