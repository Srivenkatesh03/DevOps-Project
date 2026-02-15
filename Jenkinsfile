pipeline{
    agent any
    environment {
        DOCKERHUB = "srivenkatesh04"
    }

    stages{
        stage('Git clone') {
          steps{
                git 'https://github.com/Srivenkatesh03/DevOps-Project.git'
                echo 'cloned'
          }   
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t srivenkatesh04/backend:latest ./backend'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t srivenkatesh04/frontend:latest ./frontend'
            }
        }

         stage('Push Images to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                        docker.image("${DOCKERHUB}/backend:latest").push()
                        docker.image("${DOCKERHUB}/frontend:latest").push()
                    }
                }
            }
        }
    }
}