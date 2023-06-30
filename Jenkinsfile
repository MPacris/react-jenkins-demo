pipeline {

    agent any

    environment {
            def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
            def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
            PATH = "${nodejsTool}/bin:${dockerTool}/bin:${env.PATH}"
    }

    stages {
q
        stage('Install Dependencies'){
            steps {
                sh 'npm install'
            }
        }
        
        stage('Create Production React Build'){
            steps {
                sh 'npm run-script build'
            }
        }

        

        stage('Build Docker Image'){
            steps {

                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "echo ${DOCKER_USERNAME}"
                }
                
                sh '''
                    docker build -t mpacris/react-jenkins-docker:latest .
                    docker images
                '''
            }
        }
        
        stage('Push Docker Image'){
            steps {

                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "echo ${DOCKER_USERNAME}"
                }           
            }
        }

        stage('Deploy New Image to AWS EC2'){
            steps {
                // SSH into remote server
                // Shut down the current running image
                // pull the new image that was pushed
                // Launch the new image running on remote server
            }
        }

        
    }
}