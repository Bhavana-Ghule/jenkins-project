@Library('my-shared-library') _

pipeline {
    agent {
        label 'agent-1'
    }

    stages {

        stage('Test Shared Library') {
            steps {
                hello()
            }
        }

    }
}
