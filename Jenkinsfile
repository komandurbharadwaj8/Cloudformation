pipeline {
  agent any

  environment {
    AWS_DEFAULT_REGION = 'ap-south-1'
  }
  stages {
    stage('Deploy CloudFormation') {
      steps {
        withCredentials([string(credentialsId: 'aws-credentials', variable: 'AWS_ACCESS_KEY_ID'), string(credentialsId: 'aws-credentials', variable: 'AWS_SECRET_ACCESS_KEY')]) {
          script {
            // Install AWS CLI
            sh 'pip install awscli'

            // Validate CloudFormation template
            sh 'aws cloudformation validate-template --template-body file:///home/user/AWSCloudformation/s3bucket.yml'

            // Create CloudFormation stack
            sh 'aws cloudformation create-stack --stack-name demofile --template-body file:///home/user/AWSCloudformation/s3bucket.yml' 

            // Wait for stack creation to complete
            sh 'aws cloudformation wait stack-create-complete --stack-name demofile'
          }
        }
      }
    }
  }
}
