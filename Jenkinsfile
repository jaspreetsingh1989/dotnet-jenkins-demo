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
    stage ('Restore Packages') {     
         steps {
             echo 'Restore Packages...'
             deleteDir()
             unstash 'source'
             script {
                 bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore "src\\dotnet-jenkins-demo.sln" '
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
