pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from Git...'
                // Git polling or SCM configuration in Jenkins will handle checkout
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image devops-demo'
                script {
                    // use Windows batch since Jenkins node is Windows
                    bat 'docker build -t devops-demo .'
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping and removing any existing container'
                script {
                    bat 'docker stop devops-demo || echo "no container to stop"'
                    bat 'docker rm devops-demo || echo "no container to remove"'
                }
            }
        }

        stage('Run New Container') {
            steps {
                echo 'Running new container from fresh image'
                script {
                    bat 'docker run -d -p 9090:80 --name devops-demo devops-demo'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution complete.'
        }
    }
}