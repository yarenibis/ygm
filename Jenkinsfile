pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Kaynak kodunun versiyon kontrol sisteminden çekilmesi
                git 'https://github.com/yarenibis/ygm.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Docker imajının inşa edilmesi
                script {
                    sh 'docker build -t ymsfinal .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Docker konteynerinin çalıştırılması
                script {
                    sh 'docker run -p 8090:8080 -p 4849:4848 -d ymsfinal'
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                // Docker Compose kullanarak konteynerlerin çalıştırılması
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            // Başarılı bir pipeline çalışmasından sonra yapılacak işlemler
            echo 'Pipeline completed successfully!'
        }
        failure {
            // Başarısız bir pipeline çalışmasından sonra yapılacak işlemler
            echo 'Pipeline failed!'
        }
    }
}
