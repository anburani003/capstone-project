pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = credentials('dockerhub-creds').username
        DOCKER_HUB_PASSWORD = credentials('dockerhub-creds').password
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM',
                        branches: [[name: '*/dev'], [name: '*/master']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'workspace']],
                        submoduleCfg: [],
                        userRemoteConfigs: [[url: 'https://github.com/anburani003/capstone-project.git']]]
                    )
                }
            }
        }

        stage('Build and Push Docker Image (dev)') {
            when {
                expression { env.BRANCH_NAME == 'dev' }
            }
            steps {
                script {
                    // Authenticate with Docker Hub using credentials
                    sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'

                    // Build and push the Docker image to the dev repository on Docker Hub
                    sh 'docker build -t anbuvanitha/dev:v01 .' // Replace with your Docker Hub username and dev repository name
                    sh 'docker push pipeline {
    
    agent any
    environment {
        DOCKER_HUB_USERNAME = credentials('dockerhub-creds').username
        DOCKER_HUB_PASSWORD = credentials('dockerhub-creds').password
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM',
                        branches: [[name: '*/dev'], [name: '*/master']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'workspace']],
                        submoduleCfg: [],
                        userRemoteConfigs: [[url: 'https://github.com/anburani003/capstone-project.git']]]
                    )
                }
            }
        }

        stage('Build and Push Docker Image (dev)') {
            when {
                expression { env.BRANCH_NAME == 'dev' }
            }
            steps {
                script {
                    // Authenticate with Docker Hub using credentials
                    sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'

                    // Build and push the Docker image to the dev repository on Docker Hub
                    sh 'docker build -t anbuvanitha/dev:v02 .' // Replace with your Docker Hub username and dev repository name
                    sh 'docker push anbuvanitha/dev:v02'
                }
            }
        }

        stage('Merge to Master') {
            when {
                changeset not empty: true, from: 'dev', to: 'master'
            }
            steps {
                script {
                    // Authenticate with Docker Hub using credentials
                    sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'

                    // Build and push the Docker image to the prod repository on Docker Hub
                    sh 'docker build -t anbuvanitha/dev:v02 .' // Replace with your Docker Hub username and prod repository name
                    sh 'docker push anbuvanitha/dev:v02'
                }
            }
        }
    }
}'
           
