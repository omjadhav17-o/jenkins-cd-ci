pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/omjadhav17-o/jenkins-cd-ci.git'
            }
        }
        stage('Build') {
            steps {
                dir('app') {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                dir('app') {
                    sh 'npm test'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                dir('app') {
                    sh 'docker build -t node-cicd-demo:latest .'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop node-cicd-demo || true'
                sh 'docker rm node-cicd-demo || true'
                sh 'docker run -d --name node-cicd-demo -p 3000:3000 node-cicd-demo:latest'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}