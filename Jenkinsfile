pipeline {
    options {
    skipDefaultCheckout()
}
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/core/sdk:3.1' // Specify the Docker image to use
            args '-v /var/run/docker.sock:/var/run/docker.sock' // Bind the Docker socket
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
            stage('Restore') {
            steps {
                script {
                    sh 'dotnet restore' // Restore .NET dependencies
                }
            }
        }

        // stage('Build') {
        //     steps {
        //         script {
        //             sh 'dotnet restore' // Restore .NET dependencies
        //         }
                
        //         // Build the .NET Core project
        //         //sh 'dotnet build --configuration Release'
                
        //         // Run tests
        //         //sh 'dotnet test'
                
        //         // Publish the .NET Core project
        //         //sh 'dotnet publish --configuration Release --output ./publish'
        //     }
        // }
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
