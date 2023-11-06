pipeline {
    agent any
    environment {

        DOCKERHUB_CREDENTIALS = credentials('docker_aymen')
    }
    stages {
        stage('Checkout'){
            agent any
            steps{

                git branch: 'master', url:'https://github.com/AymenFtiti1992/devopsProject.git'
            }
        }
        stage('Init'){
            steps{

                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build'){
            steps {

                sh 'docker build -t aymenftiti/springboot-app:jdk-17:$BUILD_ID -f ./Dockerfile .'
                //sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/calculator-app:$BUILD_ID'
            }
        }
        stage('Deliver'){
            steps {

                sh 'docker push aymenftiti/springboot-app:jdk-17:$BUILD_ID'
            }
        }
        stage('Cleanup'){
            steps {

            sh 'docker rmi aymenftiti/springboot-app:jdk-17:$BUILD_ID'
            sh 'docker logout'
            }
        }
    }
}