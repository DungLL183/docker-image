pipeline{
    agent linux
    options{
        buildDiscarder(logRotator(numToKeepStr:'$'))  
    }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('dung-dockerhub')
    }
    stages{
        stage('Build'){
            steps{
                sh 'docker build -t dung/dp-alpine:latest .'
            }
        }
        stage('Login'){
            steps{
                sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --pasword-stdin'
            }
        }
        stage('Push'){
            steps{
                sh 'docker push dung/dp-alpine:latest'
            }
        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}





