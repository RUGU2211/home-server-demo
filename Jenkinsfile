
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
    }
}
