pipeline {
    agent any
    stages {
        stage('SyntaxTest'){
            steps{
                sh '''
                    aws cloudformation validate-template --template-body file://vpcStack.yml
                '''
            }
        }
        stage('Build'){
            steps{
                sh '''
                    aws cloudformation deploy --stack-name vpcproduccion --template-file vpcStack.yml --capabilities CAPABILITY_NAMED_IAM
                '''
            }
        }
    }
}