pipeline {

    agent any

    environment {
            def nodejsTool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
            def dockerTool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
            PATH = "${nodejsTool}/bin:${dockerTool}/bin:${env.PATH}"
    }

    stages {

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
                
                sh '''
                    docker build -t mpacris/react-jenkins-docker:latest .
                    docker images
                '''
            }
        }
        
        stage('Push Docker Image'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    sh 'docker push mpacris/react-jenkins-docker:latest'
                }           
            }
        }

        stage('Deploy New Image to AWS EC2'){
            steps {
                sh 'echo "Deploying to EC2 instance..."'
                // SSH into remote server
                // Shut down the current running image
                // pull the new image that was pushed
                // Launch the new image running on remote server
            }
        }

        
    }
}