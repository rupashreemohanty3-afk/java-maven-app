pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "java-maven-app:1.0"
        CONTAINER_NAME = "java-app"
        HOST_PORT = "9090"
        CONTAINER_PORT = "8080"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/rupashreemohanty3-afk/java-maven-app.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh '''
                    java -version
                    mvn -version
                    mvn clean package
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
                sh 'docker run -d -p $HOST_PORT:$CONTAINER_PORT --name $CONTAINER_NAME $DOCKER_IMAGE'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline successful. App running on port 9090"
        }
        failure {
            echo "❌ Pipeline failed. Check console output."
        }
    }
}
