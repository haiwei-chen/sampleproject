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
                 stage('Build Python Wheel') {
                 steps {
                    sh 'echo $JOB_NAME'
                    sh 'python3 setup.py sdist bdist_wheel'
                    }
                 }
                stage('Upload') {
                    steps{
                    withAWS(region:'us-west-2',credentials:'ArtifactServiceAcct') {
                    // Upload files from working directory 'dist' in your project workspace
                    s3Upload(bucket:'foobar.artifacts', path:'modules/python/sampleproject/', workingDir:'dist', includePathPattern:'**/*.whl')
                }
                }
            }
        }
    }
