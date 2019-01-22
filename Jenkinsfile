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
                sshagent () {
                    sh 'GIT_SSH_COMMAND="ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no" git clone -b $BRANCH_NAME git@github.com:claudioibuildings/backend.git backend'
                }
            }
        }
    }
}