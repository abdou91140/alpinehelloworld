pipeline {

    environement {
        CONTAINER_NAME = "alpine"
    }

    parameters {
        string(name : 'IMAGE_NAME', defaultValue : 'alpine' )
        string(name : 'IMAGE_TAG', defaultValue : 'test' )
        string(name : 'DOCKERHUB_ID', defaultValue : '91140')
    }

    agent none
    
    stages {
        stage('build'){
            steps{
                script{
                    sh 'git clone https://github.com/abdou91140/alpinehelloworld.git'
                    sh 'cd alpinehelloworld'
                }
            }
            steps{
                script{
                    sh 'docker build -t ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG} .'
                }
            }
        }
    }
}