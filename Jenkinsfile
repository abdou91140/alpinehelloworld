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
            agent any
            steps {
                script {
                    sh 'docker build -t ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG} .'
                }
            }
        }
        stage('push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: '56bf1244-b4de-4241-b5e0-660edd0c864e', passwordVariable: 'password', usernameVariable: 'docker_id')]) {
                    sh 'dockerlogin -u $docker_id -p $password -password-stdin'
                    sh 'docker push ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG}' 
                    }
                 }
            }
        }
    }
}
