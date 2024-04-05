pipeline {
    environment {
        CONTAINER_NAME = 'alpine'
    }

    parameters {
        string(name : 'IMAGE_NAME', defaultValue : 'alpine')
        string(name : 'IMAGE_TAG', defaultValue : 'test')
        string(name : 'DOCKERHUB_ID', defaultValue : '91140')
    }

    agent none

    stages {
        stage('build') {
            agent none
            steps {
                script {
                    sh 'docker build -t ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG} .'
                }
            }
        }
    }
}
