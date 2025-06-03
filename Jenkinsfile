pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    }

    stages {
        stage('Clone') {
            steps {
<<<<<<< HEAD:Jenkinsfile
                git branch: 'main', url: 'https://github.com/faqi22152ti/demo-app.git'
=======
                git 'https://github.com/faqi22152ti/demo-app.git'
>>>>>>> 3ab2c44 (fix: add serviceAccount config to values.yaml and update Jenkinsfile):jenkinsfile
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
