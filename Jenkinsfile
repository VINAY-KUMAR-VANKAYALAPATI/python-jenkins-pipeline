pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'git@github.com:VINAY-KUMAR-VANKAYALAPATI/python-jenkins-pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                export PATH=$HOME/.local/bin:$PATH
                python3 -m ensurepip --default-pip
                python3 -m pip install --upgrade pip
                python3 -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 -m unittest discover'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh 'sonar-scanner'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t 2022bcd0023/python-app .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push 2022bcd0023/python-app'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker run -d -p 5000:5000 2022bcd0023/python-app
                '''
            }
        }
    }
}

