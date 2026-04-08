pipeline {
    agent { label 'docker-agent' }

    stages {
        stage('Clone code') {
            steps {
                git 'https://github.com/saurbh7586/jenkins.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t mysite .'
            }
        }

        stage('Run container') {
            steps {
                sh 'docker rm -f cont1 || true'
                sh 'docker run -d -p 8081:80 --name cont1 mysite'
            }
        }
    }
}
