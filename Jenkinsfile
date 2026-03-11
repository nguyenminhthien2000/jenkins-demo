pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:v1 .'
            }
        }
        stage('Deploy') {
            steps {
                // Xóa container cũ nếu đang chạy để tránh trùng tên
                sh 'docker rm -f my-running-app || true'
                // Chạy container mới, map cổng 8081 máy thật vào cổng 80 container
                sh 'docker run -d --name my-running-app -p 8081:80 my-app:v1'
            }
        }
    }
}
