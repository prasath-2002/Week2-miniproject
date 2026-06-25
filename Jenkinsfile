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
                    echo "Deploying new container from image"
                    // Run the new container. We'll use port 8081 to avoid conflicts.
                    sh "docker run -d -p 8081:80 --name  my-website my-portfolio-app"
                }
            }
        }
    }
}
