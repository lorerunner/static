pipeline{
    agent any
    stages {
        
        stage('Build') {
            steps {
                sh 'echo "Hello world Build"'
            }
        }
        
        stage('Lint HTML') {
            steps {
                sh 'echo "Hello world Lint Html"'
            }
        }

        stage('Upload to AWS') {
            steps {
              withAWS(region:'us-east-2',credentials:'jenkinsforaws') {
              s3Delete(bucket: 'jenkinsbuckets', path:'**/*')
              s3Upload(bucket: 'jenkinsbuckets', includePathPattern:'**/*');
              }
            }
        }
    }
}
