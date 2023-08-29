pipeline {
    agent any

    environment {
        def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
        PATH = "${nodejsTool}/bin:${dockerTool}/bin:${env.PATH}"
    }

    stages {
        
        stage('Installing Dependencies'){
            steps {
                sh '''
                    echo "Installing the dependencies..."
                    npm install
                '''
            }
        }
        stage('Build Optimized React Production Files'){
            steps {
                sh '''
                    echo "Building the production files..."
                    npm run-script build
                '''
            }
        }
        stage('Build Docker Image'){
            steps {
                sh '''
                    echo "Building Docker Images..."
                    docker build -t stevenburkard/auto-dockerize-react-app:latest .
                '''
            }
        }
        stage('Push Docker Image to Docker Hub'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                    echo "Pushing Docker images to Docker Hub..."
                    docker login -u "$DOCKER_USERNAME" --password-stdin <<< "$DOCKER_PASSWORD"
                    docker push stevenburkard/auto-dockerize-react-app:latest
                '''
                }
                
            }
        }
    }
}