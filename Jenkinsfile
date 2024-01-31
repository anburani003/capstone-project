pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image (dev)') {
            when {
                branch 'dev'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    script {
                        // Authenticate with Docker Hub using credentials
                        sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'

                        // Build and push the Docker image to the dev repository on Docker Hub
                        sh 'docker build -t anbuvanitha/dev:v02 .'
                        sh 'docker push anbuvanitha/dev:v02'
                    }
                }
            }
        }

        stage('Build and Push Docker Image (prod)') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    script {
                        // Authenticate with Docker Hub using credentials
                        sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'

                        // Build and push the Docker image to the prod repository on Docker Hub
                        sh 'docker build -t anbuvanitha/prod:v02 .'
                        sh 'docker push anbuvanitha/prod:v02'
                    }
                }
            }
        }
    }
}
