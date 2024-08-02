pipeline {
    agent any
    options {
    skipDefaultCheckout()
}

    stages {
        stage ('Checkout') {
        steps{
            echo 'Checkout...'
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
