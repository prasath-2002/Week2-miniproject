pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image"
                    sh "docker build -t my-portfolio-app ."
                }
            }
        }
        stage('Deploy Application') {
            steps {
                script {
                    echo "Checking for existing container and deploying..."
                    
                    // 1. If a container named 'my-website' is running, stop it.
                    // 2. If it exists (even if stopped), remove it.
                    // '|| true' ensures the pipeline doesn't fail if the container doesn't exist yet.
                    sh "docker stop my-website || true"
                    sh "docker rm my-website || true"
                    
                    echo "Deploying new container from image"
                    sh "docker run -d -p 8081:80 --name my-website my-portfolio-app"
                }
            }
        }
    }
}