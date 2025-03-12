pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = "docker-compose -f docker-compose.yml"
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/usermanagement.git'
            }
        }

        stage('Build & Run Docker Containers') {
            steps {
                sh "${DOCKER_COMPOSE} down"
                sh "${DOCKER_COMPOSE} build --no-cache"
                sh "${DOCKER_COMPOSE} up -d"
            }
        }

        stage('Run Backend Migrations') {
            steps {
                sh "docker exec backend_app php artisan migrate --seed"
            }
        }

        stage('Deploy Completed') {
            steps {
                echo "🚀 Deployment hoàn tất!"
            }
        }
    }
}
