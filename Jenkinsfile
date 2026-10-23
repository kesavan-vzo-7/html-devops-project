
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kesavan-vzo-7/html-devops-project.git'
            }
        }

        stage('Validate Files') {
            steps {
                sh '''
                    test -f index.html
                    test -f Dockerfile
                    echo "Required files found"
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t html-devops-site:v2 .'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                    docker rm -f html-devops-container || true
                    docker run -d \
                      --name html-devops-container \
                      --restart unless-stopped \
                      -p 8081:80 \
                      html-devops-site:v2
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    docker ps
                    echo "Deployment stage completed"
                '''
            }
        }
    }
}
