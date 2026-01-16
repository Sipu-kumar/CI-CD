pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/shaanman23/my-flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Flask Docker Image..."
                    bat "docker build -t myflaskapp:latest ."
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    echo "Stopping old container if exists..."
                    bat "docker stop flaskdemo || exit 0"
                    bat "docker rm flaskdemo || exit 0"
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    echo "Running new container on port 5000..."
                    bat "docker run -d --name flaskdemo -p 5000:5000 myflaskapp:latest"
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    echo "Waiting for app to start..."
                    sleep(5)

                    echo "Testing application on port 5000..."
                    bat "curl http://localhost:5000"
                }
            }
        }

        stage('Deploy Success') {
            steps {
                echo "Flask App is running successfully at: http://localhost:5000"
            }
        }
    }
}



