pipeline {
agent any

environment {
    IMAGE_NAME = "YOUR_DOCKERHUB_USERNAME/jenkins-cicd-demo"
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
            sh '''
                test -f index.html
                test -f Dockerfile
            '''
        }
    }

    stage('Docker Build') {
        steps {
            sh '''
                docker build -t $IMAGE_NAME:$BUILD_NUMBER .
            '''
        }
    }

    stage('Docker Push') {
        steps {
            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )
            ]) {
                sh '''
                    echo "$DOCKER_PASSWORD" | docker login \
                    -u "$DOCKER_USERNAME" --password-stdin

                    docker push $IMAGE_NAME:$BUILD_NUMBER

                    docker logout
                '''
            }
        }
    }
}

post {
    success {
        echo 'Image successfully pushed to Docker Hub!'
    }

    failure {
        echo 'Pipeline failed!'
    }
}

}
