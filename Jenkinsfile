pipeline {
    agent {
        docker {
            image 'composer:latest'
            args '--privileged' // Add privileged mode if needed for Docker-in-Docker
        }
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'composer install'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh './vendor/bin/phpunit tests'
                }
            }
        }
    }
}
