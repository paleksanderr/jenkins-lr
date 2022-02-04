#!/usr/bin/env groovy

@Library('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools {
        maven 'Maven-3.6'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {

                    buildImage('paleksander/siwy:test-1.3')
<<<<<<< HEAD
                    dockerLogin()
                    dockerPush 'paleksander/siwy:test-1.3'
=======

>>>>>>> 5bf0fdf7249f58b2ada96e80a5a2ea525181646d
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
