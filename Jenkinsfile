pipeline{
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world Build"'
            }
        }

        stage('Upload to AWS') {
            steps {
              withAWS(region:'us-east-2',credentials:'AKIAVM527RRSPB6DIVXZ') {
              s3Delete(bucket: 'jenkinsbuckets', path:'**/*')
              s3Upload(bucket: 'jenkinsbuckets', workingDir:'build', includePathPattern:'**/*');
            }
            }
        }
    }
}
