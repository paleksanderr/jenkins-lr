#!/usr/bin/env groovy

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
                        sh "docker build -t paleksander/siwy:java.2.0 ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push paleksander/siwy:java.2.0"
                    }
                }
            }
        }
        sstage('Deploy') {
            steps {
                script{
                    echo 'Deploying the application'
                }
            }
        }
    }
