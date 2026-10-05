pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t jenkins-cicd-demo:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running application tests...'
                sh 'docker run --rm jenkins-cicd-demo:latest npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Docker container...'

                sh '''
                    docker stop jenkins-cicd-demo || true
                    docker rm jenkins-cicd-demo || true
                    docker run -d --name jenkins-cicd-demo -p 3000:3000 jenkins-cicd-demo:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Jenkins CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Jenkins CI/CD Pipeline failed!'
        }
    }
}