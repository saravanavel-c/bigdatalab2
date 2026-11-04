pipeline {
    agent any

    environment {
        IMAGE = 'saravanavelc/flask-docker-app'
        TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Build Python') {
            steps {
                bat 'python -m py_compile hello.py app.py test.py'
                bat 'python hello.py'
                bat 'python test.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE%:%TAG% .'
            }
        }

        stage('Test Docker Image') {
            steps {
                bat 'docker run --rm %IMAGE%:%TAG% python -m py_compile app.py'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                    bat 'docker push %IMAGE%:%TAG%'
                }
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                bat 'docker service update --image %IMAGE%:%TAG% lab-web'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}