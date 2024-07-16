pipeline {
    agent any
    tools {
        git 'default git'
    }

    environment {
        DOCKER_COMPOSE_VERSION = '1.29.2'
        COMPOSE_FILE = 'docker-compose.yml' // Docker Compose dosya adı
        PROJECT_NAME = 'myproject' // Docker Compose proje adı
    }

    stages {
        stage('Checkout') {
            steps {
                // GitHub'dan kodu çek
                git branch: 'main', url: 'https://github.com/yarenibis/ygm.git'
            }
        }

        
    
        stage('Build') {
            steps {
                script {
                    // Docker imajını oluştur
                    docker.build('myjavaapp')
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Docker imajını başlatarak container'ı çalıştır
                script {
                    docker.run('-d -p 8080:8080 --name myjavaapp-container myjavaapp')
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline başarıyla tamamlandı. Uygulama başarıyla dağıtıldı.'
        }
        failure {
            echo 'Pipeline başarısız oldu. Hata kontrol edilmeli.'
        }
    }
}
