pipeline {
    agent any

    environment {
        DOCKERHUB = "srivenkatesh04"
    }

    stages {

        stage('Git Clone') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Srivenkatesh03/DevOps-Project.git'
                echo 'Repository cloned successfully'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh """
                docker build -t ${DOCKERHUB}/backend:latest ./backend
                """
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh """
                docker build -t ${DOCKERHUB}/frontend:latest ./frontend
                """
            }
        }

        stage('Push Images to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        docker.image("${DOCKERHUB}/backend:latest").push()
                        docker.image("${DOCKERHUB}/frontend:latest").push()
                    }
                }
            }
        }
        stage('Application deploy') {
            steps{
                sh '''
                    docker-compose down || true
                    docker-compose pull
                    docker-compose up -d
                '''
            }
        }
    }
}