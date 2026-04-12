pipeline {
    agent none

    stages {
        stage('Clone Code') {
            agent any
            steps {
                git 'https://github.com/saurbh7586/jenkins.git'
            }
        }

        stage('Deploy 5 Different Containers') {
            agent { label 'docker-agent1' }
            steps {
                sh '''
                # Junya containers na stop aani remove kara
                docker stop app1 app2 app3 app4 app5 || true
                docker rm app1 app2 app3 app4 app5 || true

                # Tumchi image build kara
                docker build -t multi-app-img .

                # --- Container 1 ---
                docker run -d -p 8081:80 --name app1 multi-app-img
                docker exec app1 sh -c "echo '<h1>Hell New Container 1 🚀</h1><p>This is my first deployed website.</p>' > /usr/share/nginx/html/index.html"

                # --- Container 2 ---
                docker run -d -p 8082:80 --name app2 multi-app-img
                docker exec app2 sh -c "echo '<h1>Hell New Container 2 🛠️</h1><p>This is my second deployed website.</p>' > /usr/share/nginx/html/index.html"

                # --- Container 3 ---
                docker run -d -p 8083:80 --name app3 multi-app-img
                docker exec app3 sh -c "echo '<h1>Hell New Container 3 🌐</h1><p>This is my third deployed website.</p>' > /usr/share/nginx/html/index.html"

                # --- Container 4 ---
                docker run -d -p 8084:80 --name app4 multi-app-img
                docker exec app4 sh -c "echo '<h1>Hell New Container 4 ⚡</h1><p>This is my fourth deployed website.</p>' > /usr/share/nginx/html/index.html"

                # --- Container 5 ---
                docker run -d -p 8085:80 --name app5 multi-app-img
                docker exec app5 sh -c "echo '<h1>Hell New Container 5 ✅</h1><p>This is my fifth deployed website.</p>' > /usr/share/nginx/html/index.html"

                docker ps
                '''
            }
        }
    }
}
