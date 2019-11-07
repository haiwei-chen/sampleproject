pipeline {
         agent any
        
         stages {
                 stage('Install Depedancies') {
                 steps {
                     withEnv(["HOME=${env.WORKSPACE}"]){
                     sh 'pip install pytest'
                     }        
                    }
                 }
                 stage('Running Tests') {
                      steps {
                       withEnv(["HOME=${env.WORKSPACE}"]){
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
