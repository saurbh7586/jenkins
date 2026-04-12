pipeline {
    agent none

    stages {
        stage('Clone Code') {
            agent any
            steps {
                git 'https://github.com/saurbh7586/jenkins.git'
            }
        }

        stage('Deploy 5 Real Different Apps') {
            agent { label 'docker-agent1' }
            steps {
                sh '''
                # 1. Junya containers na stop aani remove kara
                docker stop app-nginx app-apache app-redis app-mysql app-alpine || true
                docker rm app-nginx app-apache app-redis app-mysql app-alpine || true

                # 2. Nginx Web Server (Port 8081)
                docker run -d -p 8081:80 --name app-nginx nginx:latest

                # 3. Apache HTTPD Server (Port 8082)
                docker run -d -p 8082:80 --name app-apache httpd:latest

                # 4. Redis In-Memory Database (Port 6379)
                docker run -d -p 6379:6379 --name app-redis redis:latest

                # 5. MySQL Database (Port 3306)
                docker run -d -p 3306:3306 --name app-mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest

                # 6. Alpine Linux (Lightweight OS)
                docker run -d --name app-alpine alpine tail -f /dev/null

                # Final Status
                docker ps
                '''
            }
        }
    }
}
