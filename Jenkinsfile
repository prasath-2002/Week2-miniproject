pipeline {
    // Run on any available Jenkins agent
    agent any

    // Environment variables available to all stages
    environment {
        // name of the Docker image
        IMAGE_NAME = 'logaprasath/portfolio'
        // Use a consistent name for the running container
        CONTAINER_NAME = 'my-portfolio-website'
    }

    stages {
        // STAGE 1: Build the Docker image
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the image and tag it with the image name and build number
                    // e.g., 'logaprasath/portfolio:1'
                    echo "Building Docker image: ${IMAGE_NAME}:${BUILD_NUMBER}"
                    sh "sudo docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
                }
            }
        }

        // STAGE 2: Clean up old containers
        stage('Remove Old Container') {
            steps {
                echo "Stopping and removing old container if it exists..."
                // This command will not fail if the container doesn't exist
                sh "sudo docker stop ${CONTAINER_NAME} || true"
                sh "sudo docker rm ${CONTAINER_NAME} || true"
            }
        }

        // STAGE 3: Deploy the new version
        stage('Deploy Application') {
            steps {
                script {
                    echo "Deploying new container from image ${IMAGE_NAME}:${BUILD_NUMBER}"
                    // Run the new container. We'll use port 8081 to avoid conflicts.
                    sh "sudo docker run -d -p 8081:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${BUILD_NUMBER}"
                }
            }
        }
    }

    // This block runs after the pipeline finishes, regardless of success or failure
    post {
        always {
            echo "Pipeline finished. Cleaning up old images..."
            // Best practice: remove dangling images to save disk space
            sh "sudo docker image prune -f"
        }
    }
}
