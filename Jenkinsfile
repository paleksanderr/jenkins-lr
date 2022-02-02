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
    
         stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t paleksander/siwy:fff ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push nanajanashia/demo-app:fff"
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
