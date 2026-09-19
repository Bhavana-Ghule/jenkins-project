pipeline {
    agent {label "agent-1"}

    environment {
        APP_PATH = "/home/ubuntu/workspace/"
        IMAGE_NAME = "nginx"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('clone'){
            steps{
                echo "cloning project from github to jenkins-server"
                git branch: 'main',
                credentialsId: 'github-cred',
                url: 'https://github.com/Bhavana-Ghule/jenkins-project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                dir("${APP_PATH}") {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]){
                sh " docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD} "
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
