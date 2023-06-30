pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh 'echo "Building the application"'
                sh 'npm install'
            }
        }

        stage('Docker'){
            steps {
                sh 'echo "Dockerizing the application"'
            }
        }

        
    }
}