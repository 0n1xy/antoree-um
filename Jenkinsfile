pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose -f docker-compose.yml"
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/0n1xy/antoree-um.git'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                sh "docker-compose stop backend frontend"
            }
        }

        stage('Build & Run Docker Containers') {
            steps {
                sh "${DOCKER_COMPOSE} build --no-cache"
                sh "${DOCKER_COMPOSE} up -d"
            }
        }

        stage('Run Backend Migrations') {
            steps {
                sh '''
                echo "🔄 Chờ MySQL khởi động..."
                while ! docker exec backend_app mysqladmin ping -h"database" --silent; do
                    sleep 2
                done
                echo "✅ MySQL đã sẵn sàng!"
                docker exec backend_app php artisan migrate --seed
                '''
            }
        }

        stage('Deploy Completed') {
            steps {
                echo "🚀 Deployment hoàn tất!"
            }
        }
    }
}
