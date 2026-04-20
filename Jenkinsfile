pipeline {
    agent any

    tools {
        maven 'mymaven'
        jdk   'myjdk'
    }

    environment {
        IMAGE_NAME     = "sample-webapp"
        CONTAINER_NAME = "sample-webapp-container"
    }

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repository'
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop %CONTAINER_NAME% || exit 0'
                bat 'docker rm %CONTAINER_NAME% || exit 0'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 8087:8080 --name %CONTAINER_NAME% %IMAGE_NAME%'
            }
        }
    }
}
