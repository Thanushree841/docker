pipeline {
    agent { label 'docker' }

    environment {
        DOCKER_REPO_CREDENTIALS = '26eb1a48-34cd-4b4c-852c-c08ff0eadcb7'
        DOCKER_IMAGE = '9148092892/thanu'          
        GIT_REPO = 'https://github.com/Shri19-web/Docker.git'
        BRANCH = 'main'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository from ${GIT_REPO}"
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage
