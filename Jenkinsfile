pipeline {
    agent any

    environment {
        IMAGE_NAME     = "sample-webapp"
        CONTAINER_NAME = "sample-webapp-container"
    }

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repository'
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build WAR') {
            steps {
                echo 'Building project using Maven'
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container if exists'
                bat "docker stop %CONTAINER_NAME% || exit 0"
                bat "docker rm %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running new container'
                bat "docker run -d -p 8088:8081 --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
