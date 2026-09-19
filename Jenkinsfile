pipeline {
    agent { label "agent-1" }

    environment {
        IMAGE_NAME = "sonu/nginx"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Cloning project from GitHub to Jenkins server"

                git branch: 'main',
                    credentialsId: 'github-cred',
                    url: 'https://github.com/Bhavana-Ghule/jenkins-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USERNAME" \
                        --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
}
