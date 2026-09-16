pipeline{
    
    agent any

      stages {
        stage('clone'){
           steps{
                echo "cloning project from github to jenkins-server"
                git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/Bhavana-Ghule/Jenkins.git'
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
