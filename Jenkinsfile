pipeline {
 agent {
  docker {
   image 'python:3.7.4-alpine3.9'
   args '-v /tmp:/tmp'
  }
 }
 stages {
  stage('Install Depedancies') {
   steps {
    withEnv(["HOME=${env.WORKSPACE}"]) {
     sh 'pip install pytest --user'
    }
   }
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
   sh 'python3.7 setup.py sdist bdist_wheel'
  }
 }
 stage('Upload') {
  steps {


   withAWS(region: 'us-west-2', credentials: 'ArtifactServiceAcct') {


    // Upload files from working directory 'dist' in your project workspace
    s3Upload(bucket: 'foobar.artifacts', path: 'modules/python/sampleproject/', workingDir: 'dist', includePathPattern: '**/*.whl')
   }
  }
 }
}
}
