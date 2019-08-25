pipeline {
  agent any
  stages {

  stage('Build') {
    steps {
      sh 'echo "Hello world"'
    }
  }

    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    stage('Upload to AWS') {
      steps {
        withAWS(region: 'us-east-2', credentials: 'jenkinsforaws') {
          s3Upload(bucket: 'jenkinsbuckets', includePathPattern: '**/*')
        }
      }
    }



    stage('Scan') {
    steps{
        docker.build("static-app")
        aquaMicroscanner imageName: 'static-app', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
     }
     }

  }
}
