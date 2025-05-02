pipeline {
    agent any

    // environment {
    //     DOCKER_IMAGE = 'ubuntu/simple-maven-app'
    //     DOCKER_CONTAINER = 'simple-maven-app'
    // }
    environment {
        JAR_FILE = 'target/my-app.jar'  // Adjust this based on the actual JAR name
        APP_PORT = '8081'
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

        // stage('Build Docker Image') {
        //     steps {
        //         sh 'docker build -t $DOCKER_IMAGE .'
        //     }
        // }

        // stage('Run Docker Container') {
        //     steps {
        //         sh '''
        //             docker rm -f $DOCKER_CONTAINER || true
        //             docker run -d --name $DOCKER_CONTAINER -p 8081:8081 $DOCKER_IMAGE
        //         '''
        //     }
        // }

        stage('Run Application') {
            steps {
                sh '''
                    pkill -f $JAR_FILE || true
                    nohup java -jar $JAR_FILE --server.port=$APP_PORT > app.log 2>&1 &
                '''
                echo "Application started on port $APP_PORT"
            }
        }
    }

    post {
        failure {
            echo 'Build failed!'
        }
    }
}
