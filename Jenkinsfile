pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out successfully'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Checking application files'

                sh '''
                    test -f index.html
                    test -f Dockerfile
                '''
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
