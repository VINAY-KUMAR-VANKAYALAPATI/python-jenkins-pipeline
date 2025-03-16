pipeline {
    agent any
    environment {
        SONARQUBE_URL = 'http://localhost:9000'  // Change if your SonarQube is hosted elsewhere
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'git@github.com:VINAY-KUMAR-VANKAYALAPATI/python-jenkins-pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'python3 -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 -m unittest discover'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Ensure "SonarQube" matches the name configured in Jenkins
                    sh '''
                        sonar-scanner \
                            -Dsonar.projectKey=python-jenkins-pipeline \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=$SONARQUBE_URL \
                            -Dsonar.login=$SONARQUBE_TOKEN
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t 2022bcd0023/python-jenkins-pipeline:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker login -u 2022bcd0023 -p Vinay@2004'
                sh 'docker push 2022bcd0023/python-jenkins-pipeline:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                s

