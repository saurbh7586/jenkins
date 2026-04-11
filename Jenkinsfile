pipeline {
    agent none

    stages {
        stage('Clone Code') {
            agent any
            steps {
                git 'https://github.com/saurbh7586/jenkins.git'
            }
        }

        stage('Deploy on Both Agents') {
            parallel {
                stage('Agent1 Deploy') {
                    agent { label 'docker-agent1' }
                    steps {
                        sh '''
                        echo "Deploying on Agent1"
                        # कंटेनरचे नाव 'mysite1' करा
                        docker stop mysite1 || true && docker rm mysite1 || true
                        docker build -t mysite-img .
                        docker run -d -p 8081:80 --name mysite1 mysite-img
                        '''
                    }
                }

                stage('Agent2 Deploy') {
                    agent { label 'docker-agent2' }
                    steps {
                        sh '''
                        echo "Deploying on Agent2"
                        # कंटेनरचे नाव 'mysite2' करा
                        docker stop mysite2 || true && docker rm mysite2 || true
                        docker build -t mysite-img .
                        docker run -d -p 8082:80 --name mysite2 mysite-img
                        '''
                    }
                }
            }
        }
    }
}
