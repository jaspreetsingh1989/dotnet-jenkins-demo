pipeline {
    options {
    skipDefaultCheckout()
}
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
        stage('Fix Permissions') {
            steps {
                script {
                    // Change ownership to Jenkins user
                    sh 'chown -R 1000:1000 src/dotnet-jenkins-demo'
                    // Ensure Jenkins user has write permissions
                    sh 'chmod -R u+w src/dotnet-jenkins-demo'
                }
            }
        }
        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }
        stage('Setup') {
            steps {
                script {
                    sh 'mkdir -p /tmp/.dotnet && chown -R 1000:1000 /tmp/.dotnet'
                    sh 'mkdir -p /tmp/.nuget/packages && chown -R 1000:1000 /tmp/.nuget/packages'
                }
            }
        }
        stage ('Checkout') {
        steps{
            script{
            checkout(scm)
            sh 'chown -R 1000:1000 $WORKSPACE'
            stash includes: '**', name: 'source', useDefaultExcludes: false
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
                deleteDir()
                unstash 'source'
                dir('src\\dotnet-jenkins-demo'){
                script {
                    sh 'dotnet build' // Build the .NET project
                }
                }
            }
        }
        stage('Test') {
            steps {
                dir('src\\dotnet-jenkins-demo'){
                script {
                    sh 'dotnet test' // Run tests
                }
                }
            }
        }
        stage('Publish') {
            steps {
                deleteDir()
                unstash 'source'
                dir('src\\dotnet-jenkins-demo'){
                script {
                    sh 'dotnet publish -o out' // Publish the .NET project
                }
                }
            }
        }
    }
}
