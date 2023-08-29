pipeline {
    agent any

    enviornment {
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
                    
                '''
            }
        }
        stage('Build Docker Image'){
            steps {
                sh 'echo "Building Docker Images..."'
            }
        }
        stage('Push Docker Image to Docker Hub'){
            steps {
                sh 'echo "Pushing Docker images to Docker Hub..."'
            }
        }
    }
}