pipeline {
    agent {
        label 'agent-demo'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch : 'main', url: 'https://github.com/veer-H/dockercompose.git'
            }
        }
        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker compose up -d'
                }
            }
        }
    }
    post {
        always {
            script {
                sh 'docker compose down'
            }
        }
    }
}
