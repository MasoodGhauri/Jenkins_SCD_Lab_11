pipeline {
    agent any
    
    tools{
        nodejs 'jenkinsNode'
    }

    environment {
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git 'https://github.com/MasoodGhauri/Jenkins_SCD_Lab_11.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                // Install dependencies for the frontend
                sh 'npm install'
            }
        }

        stage('Building Docker Image') {
            steps {
                // Build the docker image for  React frontend
               sh 'docker build -t jenkinsproject_scd_11 .'
            }
        }

        stage('Running Image in Container') {
            steps {
                // Run Image of the React application in container
               sh 'docker run -d --name jenkinsproject_scd_11_container -p 3000:3000 jenkinsproject_scd_11'
            }
        }

        stage('Pushing Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_HUB_CREDENTIALS}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    // Push the image to Docker Hub
                    sh 'docker push jenkinsproject_scd_11'
                }
            }
        }
    }
}