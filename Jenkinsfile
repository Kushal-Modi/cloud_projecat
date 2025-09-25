pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/Kushal-Modi/cloud_projact.git'
            }
        }

        stage('Build') {
            steps {
                // Example for Java project
                // sh 'mvn clean install -DskipTests'

                // Example for Node.js project
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Example for Java project
                //sh 'mvn test'

                // Example for Node.js project
                 sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                // Right now just echo, later we can replace with real deployment
                echo "Deploying application..."
            }
        }
    }
}
