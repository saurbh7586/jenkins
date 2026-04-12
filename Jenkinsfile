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
                # Junya containers na stop aani remove kara
                docker stop app-nginx app-apache app-redis app-mysql app-alpine || true
                docker rm app-nginx app-apache app-redis app-mysql app-alpine || true

                # 1. Nginx Web Server (Static Content)
                docker run -d -p 8081:80 --name app-nginx nginx:latest

                # 2. Apache HTTPD (Alternative Web Server)
                docker run -d -p 8082:80 --name app-apache httpd:latest

                # 3. Redis (In-Memory Database / Cache)
                docker run -d -p 6379:6379 --name app-redis redis:latest

                # 4. MySQL Database (Backend Database)
                # Password 'root' dila aahe
                docker run -d -p 3306:3306 --name app-mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest

                # 5. Alpine (Lightweight Linux Container)
                # Ha container run houn ek message print karel
                docker run -d --name app-alpine alpine tail -f /dev/null

                echo "--- All 5 Different Apps Deployed ---"
                docker ps
                '''
            }
        }
    }
}
