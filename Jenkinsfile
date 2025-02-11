pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-webserver"
        CONTAINER_NAME = "webserver_container"
        PORT = "8081"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/vimal1721/sinmple-web-server.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:80 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "Webserver deployed successfully at http://localhost:${PORT}"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
