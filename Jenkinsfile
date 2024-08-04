pipeline {
    agent any
    options {
    skipDefaultCheckout()
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

        stage('Build') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:3.1'
                    args '-v /var/jenkins_home:/var/jenkins_home'
                }
            }
            steps {
                // Restore .NET Core packages
                sh 'dotnet restore'
                
                // Build the .NET Core project
                //sh 'dotnet build --configuration Release'
                
                // Run tests
                //sh 'dotnet test'
                
                // Publish the .NET Core project
                //sh 'dotnet publish --configuration Release --output ./publish'
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
