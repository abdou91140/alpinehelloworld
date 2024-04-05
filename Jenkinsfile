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
            agent any
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: '56bf1244-b4de-4241-b5e0-660edd0c864e', passwordVariable: 'password', usernameVariable: 'docker_id')]) {
                    sh 'echo $password | docker login -u $docker_id --password-stdin'
                    sh 'docker push ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG}' 
                    }
                 }
            }
        }
        stage('deploiement') {
            agent any
            steps {
                script {
                    sh 'docker run -p 8088:5000 -e $PORT:5000 -d --name=$CONTAINER_NAME ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG}'
                }
            }
        }
    }
}
