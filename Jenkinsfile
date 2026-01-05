pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main',
                url: 'https://github.com/admin105-sudo/Repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t username/myapp:latest .'
            }
        }

        stage('DockerHub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push username/myapp:latest'
            }
        }
    }
}
