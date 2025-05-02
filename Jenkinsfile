pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ubuntu/simple-maven-app'
        DOCKER_CONTAINER = 'simple-maven-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Thakshila-Bandara/simple-java-maven-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f $DOCKER_CONTAINER || true
                    docker run -d --name $DOCKER_CONTAINER -p 8081:8081 $DOCKER_IMAGE
                '''
            }
        }
    }

    post {
        failure {
            echo 'Build failed!'
        }
    }
}
