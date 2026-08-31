pipeline {
agent any

environment {
    IMAGE_NAME = "jenkins-cicd-demo"
}

stages {

    stage('Checkout') {
        steps {
            echo 'Checking out source code'
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

    stage('Docker Build') {
        steps {
            echo 'Building Docker image'

            sh '''
                docker build -t $IMAGE_NAME:$BUILD_NUMBER .
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
