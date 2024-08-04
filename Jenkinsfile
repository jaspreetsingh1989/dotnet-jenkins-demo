pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:3.1'
            args '-v /var/jenkins_home:/var/jenkins_home'
        }
    }
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
            stage('Restore Packages') {
            steps {
                script {
                    // Restore .NET Core 3.1 packages
                    sh 'dotnet restore'
                }
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
