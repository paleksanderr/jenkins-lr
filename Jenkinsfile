pipeline {
    agent any
    tools {
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
    
        stage("Build Docker image") {
            steps {
                script{
                    echo "Bulding the Docker image...."
                    withCredentials([usernamePassword(credentialsId: 'docer-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')])
                    {
                       sh 'Docker build -t -f paleksander/siwy:jma-2.0 .'
                       sh "echo $PASS | Docker login -u $USER , --password-stdin"
                       sh 'Docker push paleksander/siwy:jma-2.0'
                    }
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
