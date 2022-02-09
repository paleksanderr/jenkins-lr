#!/usr/bin/env groovy

@Library('jenkins-shared-library')
def gv

pipeline {
    agent any
    tools {
        maven 'Maven-3.6'
    }
    stages {
          stage("increment version") {
                    steps {
                        script {
                            echo 'incremeting app version...'
                            sh 'mvn build-helper:parse-version versions:set \
                            -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                            versions:commit'
                            def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                            def version = matcher[0][1]
                            env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                        }
                    }
                }
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
                    sh 'mvn clean package'
                }
            }
        }
        stage("build and push image") {
            steps {
                script {

                    buildImage "paleksander/siwy:$IMAGE_NAME"
                    dockerLogin()
                    dockerPush "paleksander/siwy:$IMAGE_NAME"

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
         stage("commit version update") {
                    steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'git2', passwordVariable: 'PASS', usernameVariable: 'USER')]) {



                            sh "git remote set-url origin https://${USER}:${PASS}@gitlab.com/pawel.aleksander/jenkins-lr.git"







                            sh 'git add .'
                            sh 'git commit -m "caly pipeline zrobiony!!!"'
                            sh 'git push origin HEAD:main'
                            }
                        }
                    }
         }

    }
}
