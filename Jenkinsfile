pipeline {
    agent any

    stages {
        stage ('Checkout') {
        steps{
            echo 'Checkout...'
            script {
                    def workspaceDir = pwd()
                    echo "Workspace Directory: ${workspaceDir}"
                }
            checkout(scm)
            stash includes: '**', name: 'source', useDefaultExcludes: false
        }
    }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
