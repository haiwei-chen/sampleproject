pipeline {
         agent any
        
         stages {
                 stage('Install Depedancies') {
                 steps {
                     sh 'PYENV_HOME=$WORKSPACE/.pyenv/'
                     sh 'virtualenv --no-site-packages $PYENV_HOME'
                     sh 'source $PYENV_HOME/bin/activate'
                     sh 'pip install -U pytest'
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
                    sh 'python setup.py sdist bdist_wheel'
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
