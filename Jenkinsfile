pipeline {
    agent {label 'docker'}

    environment {
        DOCKER_REPO_CREDENTIALS = '6c0285c6-6495-4e45-91d2-9c7e59e91cbf'
        DOCKER_IMAGE = '148092892/kubernetes'          
        GIT_REPO = 'https://github.com/Thanushree841/kubernetes.git'
        BRANCH = 'main' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository from ${GIT_REPO}"
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }

       stage('Build Docker Image') {
            steps {
                script {
                    IMAGE_TAG_LATEST = "${DOCKER_IMAGE}:latest"
                    echo "Building Docker image with tag: ${IMAGE_TAG_LATEST}"
                    sh "docker build -t ${IMAGE_TAG_LATEST} ."
                }
            }
        }

        stage('Authenticate with Docker Registry') {
            steps {
                script {
                    echo "Logging in to Docker registry"
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_REPO_CREDENTIALS}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    echo "Pushing images to registry"
                    echo "IMAGE_TAG_LATEST: ${IMAGE_TAG_LATEST}"
                    sh "docker push ${IMAGE_TAG_LATEST}"
                }
            }
        }
    }

    post {
        success {
            echo " Deployment succeeded!"
        }
        failure {
            echo " Deployment failed!"
        }
    }
}
         
