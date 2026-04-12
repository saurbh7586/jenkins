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
                # 1. Junya sagle containers stop aani remove kara
                docker stop app1 app2 app3 app4 app5 || true
                docker rm app1 app2 app3 app4 app5 || true

                # 2. ATA BUILD KARAYCHI GARAJ NAHI (No docker build)
                # Direct veg-veglya images vapra
                
                docker run -d -p 8081:80 --name app1 nginx:latest
                docker run -d -p 8082:80 --name app2 httpd:latest
                docker run -d -p 6379:6379 --name app3 redis:latest
                docker run -d -p 3306:3306 --name app4 -e MYSQL_ROOT_PASSWORD=root mysql:latest
                docker run -d -p 8083:80 --name app5 tutum/hello-world

                # 3. Final Check
                docker ps
                '''
            }
        }
    }
}
