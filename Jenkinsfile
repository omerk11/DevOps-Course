pipeline {
    agent any
    
    parameters { 
        choice(name: 'Script_Choice', choices: ['3', '2', '1'], description: '1 - Frontend \n 2 - Backend \n 3 - Default - Combined') }
    stages {
        stage('Pull Code') {
            steps {
                script {
                    properties([pipelineTriggers([pollSCM('*/30 * * * *')])])
                }
                git 'https://github.com/omerk11/DevOps-Course.git'
            }
        }
        stage('run rest app server ') {
            steps {
                script {
                    sh 'nohup python3.8 rest_app.py &'

                }
            }
        }
        stage('run web app server') {
            steps {
                script {
                    sh 'nohup python3.8 web_app.py &'

                }
            }
        }
        stage('Choice') {
            steps {
                script {
                    if (params.Script_Choice == '1'){
                        sh 'python frontend_testing.py'
                    }else if (params.Script_Choice == '2'){
                        sh 'python backend_testing.py'
                    }else{
                        sh 'python combined_testing.py'
                   }
                }
            }
        stage('run clean environmant ') {
            steps {
                script {
                    sh ' python3.8 clean_environment.py'

                }
            }
        }
    }
}

