pipeline {
    agent none

    stages {
        stage('Clone Code') {
            agent any
            steps {
                git 'https://github.com/saurbh7586/jenkins.git'
            }
        }

        stage('Deploy 5 Containers on Single Node') {
            agent { label 'docker-agent1' }
            steps {
                sh '''
                docker stop app1 app2 app3 app4 app5 mysite1 mysite2 mysite || true
                docker rm app1 app2 app3 app4 app5 mysite1 mysite2 mysite || true

                docker build -t multi-app-img .

                docker run -d -p 8081:80 --name app1 multi-app-img
                docker run -d -p 8082:80 --name app2 multi-app-img
                docker run -d -p 8083:80 --name app3 multi-app-img
                docker run -d -p 8084:80 --name app4 multi-app-img
                docker run -d -p 8085:80 --name app5 multi-app-img

                docker ps
                '''
            }
        }
    }
}
