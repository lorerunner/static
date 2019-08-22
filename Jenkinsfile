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
              withAWS(region:'us-east-2',credentials:'jenkinsforaws') {
              s3Delete(bucket: 'jenkinsbuckets', path:'**/*')
              s3Upload(bucket: 'jenkinsbuckets', path:'index.html');
            }
            }
        }
    }
}
