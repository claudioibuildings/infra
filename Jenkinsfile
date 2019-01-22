env.CURRENT_ENV = 'stage'
if (env.BRANCH_NAME == 'release/prod') {
    env.CURRENT_ENV = 'prod'
}

pipeline {
    agent any

    environment {
        CONTAINER_REGISTRY_BASE = 'registry:5000'
    }

    stages {

        stage('Checkout') {

            steps {

                // Checkout deploy repo.
                checkout scm

                // Checkout app repo.
                dir('backend') {
                    git branch: ${BRANCH_NAME}, url: 'git@github.com:claudioibuildings/backend.git'
                }
            }
        }
    }
}