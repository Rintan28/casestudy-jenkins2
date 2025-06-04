pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Rintan28/casestudy-jenkins2.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                docker build -t $DOCKERHUB_CREDENTIALS_USR/demo-app:latest .
                '''
            }
        }
        stage('Push to DockerHub') {
            steps {
                sh 'docker push $DOCKERHUB_CREDENTIALS_USR/demo-app:latest'
            }
        }
        stage('Deploy to Minikube') {
            steps {
                sh 'helm upgrade --install flask-app ./helm-chart --set image.repository=$DOCKERHUB_CREDENTIALS_USR/demo-app --set image.tag=latest'
            }
        }
    }
}
