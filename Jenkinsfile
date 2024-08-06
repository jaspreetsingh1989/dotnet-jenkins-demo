pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/core/sdk:3.1'
            args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOTNET_CLI_HOME = '/tmp/.dotnet'
        NUGET_PACKAGES = '/tmp/.nuget/packages'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    sh 'mkdir -p /tmp/.dotnet && chown -R 1000:1000 /tmp/.dotnet'
                    sh 'mkdir -p /tmp/.nuget/packages && chown -R 1000:1000 /tmp/.nuget/packages'
                }
            }
        }
        // stage('Verify Docker') {
        //     steps {
        //         script {
        //             sh 'docker version' // Verify Docker CLI access
        //         }
        //     }
        // }
        stage('Restore') {
            steps {
                deleteDir()
                unstash 'source'
                script {
                    sh 'dotnet restore "src\\dotnet-jenkins-demo.sln"' // Restore .NET dependencies
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'dotnet build' // Build the .NET project
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'dotnet test' // Run tests
                }
            }
        }
        stage('Publish') {
            steps {
                script {
                    sh 'dotnet publish -o out' // Publish the .NET project
                }
            }
        }
    }
}
