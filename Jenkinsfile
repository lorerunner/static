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

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
    steps{
      script{
        docker.build("devops/static-app")
      }
    }
    }


    stage('Scan') {
    steps{
        aquaMicroscanner imageName: 'devops/static-app', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
     }
     }

  }
}
