pipeline {
    agent any

    environment {
        // Replace with your Docker Hub username and desired image name
        DOCKER_IMAGE = "aniruddhaahale/materialsproject/devops:latest" // Update this to your desired Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the code from the GitHub repository
                git 'https://github.com/aniruddhaahale/WIT_POE.git' // Replace this with your actual GitHub repository URL
            }
        }

        stage('Build') {
            steps {
                // Compile the Java application using Maven
                bat 'mvn clean package'
            }
        }

        stage('Dockerize') {
            steps {
                // Build the Docker image
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Login and push the image to Docker Hub using credentials stored in Jenkins
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'aniruddhaahale', passwordVariable: 'Aniruddha009@')]) {
                    // Docker login to Docker Hub
                    bat 'docker login -u $aniruddhaahale -p $Aniruddha009@'
                    // Push the image to Docker Hub
                    bat "docker push ${env.DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images to save space after the pipeline finishes
            bat 'docker rmi ${DOCKER_IMAGE} || true'
        }
    }
}
