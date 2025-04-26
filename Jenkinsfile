pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dipeshagarwal' // Credentials ID you created
        DOCKERHUB_USERNAME = 'dipeshagarwal'     // Replace it
        IMAGE_NAME = 'webapp_exam'                     // Replace it
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the GitHub repository...'
                git url: 'https://github.com/dipeshagarwaaal/Node_App.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${dipeshagarwal}/${webapp_exam}:latest ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                echo 'Logging into Docker Hub...'
                withCredentials([usernamePassword(credentialsId: "${dipeshagarwal}", usernameVariable: 'dipeshagarwal', passwordVariable: 'docker@25')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                sh "docker push ${dipeshagarwal}/${webapp_exam}:latest"
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh "docker rmi ${dipeshagarwal}/${webapp_exam}:latest || true"
        }
    }
}
