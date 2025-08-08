pipeline {
    agent any

    environment {
        COMPOSE_FILE = "docker-compose.yml"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/3-tier-crud-app.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'docker-compose exec web python manage.py migrate'
            }
        }

        stage('Collect Static Files') {
            steps {
                sh 'docker-compose exec web python manage.py collectstatic --noinput'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
