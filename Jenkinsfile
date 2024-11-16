pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/dynamic-website-project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dynamic-website .'
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    sh 'docker tag dynamic-website your-dockerhub-username/dynamic-website:latest'
                    sh 'docker push your-dockerhub-username/dynamic-website:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f kubernetes/deployment.yaml'
            }
        }
    }
}
