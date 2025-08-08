
pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "crud_app"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/GAUTAM7978/3-tire-crud-app.git'
            }
        }

        stage('Build Containers') {
            steps {
                echo 'Building Docker containers...'
                sh 'docker-compose -f docker-compose.yml build'
            }
        }

        stage('Run Migrations') {
            steps {
                echo 'Running Django migrations...'
                sh 'docker-compose run web python manage.py migrate'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Django tests...'
                sh 'docker-compose run --rm web python manage.py test'
            }
        }

        stage('Start App') {
            steps {
                echo 'Starting the full stack...'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker-compose down --remove-orphans'
        }
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs.'
        }
    }
}
