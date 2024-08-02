pipeline {
    agent any
    options {
    skipDefaultCheckout()
}

    stages {
        stage ('Checkout') {
        steps{
            echo 'Checkout...'
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
