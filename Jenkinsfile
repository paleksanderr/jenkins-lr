def gv

pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', "1.2.0", "1.3.0"], description: '')
        boolenParam(name: 'executeTest', defaultValue: true, description: '')
    }

    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage('build') {
             when {
                expression {
                    params.executeTests
                }
            }
            
            steps{
                script {
                    gv.buildApp()
                }
                echo 'Testing the app...'
            }
        }   
        }
        stage('test') {
             
            steps {
                script {
                    gv.testApp()
                }
                echo 'Deploying....'

            }
        stage('deploy') {
             
            steps {
                script {
                    gv.deployApp()
                }
                echo 'Deploying....'

            }


      
    }
    
}