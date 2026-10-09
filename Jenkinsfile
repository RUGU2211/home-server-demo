
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pipeline loaded from SCM.'
                sh 'git rev-parse --short HEAD'
            }
        }

        stage('Validate') {
            steps {
                sh '''
                    test -f Dockerfile
                    test -f index.html
                    echo "Website files validated."
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t home-web:latest .'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                    docker stop home-web || true
                    docker rm home-web || true
                    docker run -d \
                        --name home-web \
                        --restart unless-stopped \
                        -p 8081:80 \
                        home-web:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps --filter name=home-web'
                echo 'Website deployment completed.'
            }
        }
    }
}

