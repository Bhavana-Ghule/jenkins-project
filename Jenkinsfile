pipeline{
    
    agent any

      stages {
        stage('clone'){
           steps{
                echo "cloning project from github to jenkins-server"
                git branch: 'main',
                credentialsId: 'webhook',
                url: 'https://github.com/Bhavana-Ghule/jenkins-project.git'
             }
          }
         stage('build'){
            steps{
                 echo "building code from dockerfile to docker-image"
                 sh 'touch raj'
             }
          }
      }
}
