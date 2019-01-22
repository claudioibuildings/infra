env.CURRENT_ENV = 'stage'
if (env.BRANCH_NAME == 'release/prod') {
    env.CURRENT_ENV = 'prod'
}

pipeline {
    agent any

    environment {
        CONTAINER_REGISTRY_BASE = '0.0.0.0:5000'
    }

    stages {

        stage('Checkout') {

            steps {

                // Checkout deploy repo.
                checkout scm

                // Checkout app repo.
                dir('backend') {
                    git branch: env.BRANCH_NAME, url: 'git@github.com:claudioibuildings/backend.git'
                }
            }
        }

        stage('build') {
            steps {
                sh "docker-compose -f docker-compose.yml build"
            }
        }

        stage('deploy') {
            steps {
                sh "docker-compose -f docker-compose.yml push"
                sh "docker-compose -f docker-compose.yml up -d"
            }
        }
    }
}