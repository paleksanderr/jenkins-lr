pipeline {
    agent any
    tolls {
       maven 'Maven-3.6'
    }
    stages {
        stage('Build jar') {
            steps {
                script{
                    echo 'Bulding the application...'
                    sh 'mvn package'
                }
            }
        }
    
        stage('Build Docker image') {
            steps {
                script{
                    echo 'Bulding the Docker image....'
                    sshagent(credentials: [1])
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script{
                    echo 'Deploying the application'
                }
            }
        }
    }
    
}