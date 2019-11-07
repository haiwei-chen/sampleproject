pipeline {
         agent {
                docker {
                image 'python:3.7.4-alpine3.9'
                args  '-v /tmp:/tmp --user 0:0'
            }
        }
         stages {
                 stage('Install Depedancies') {
                 steps {
                     sh 'pip install pytest'
                    }
                 }

                 stage('Running Tests') {
                 steps {
                    sh 'py.test tests'
                    }
                }                
        }
    }
