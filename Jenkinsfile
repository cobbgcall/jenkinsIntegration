pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access')
    }
    node{
        withCredentials([strig(credentialsId: 'aws-access-key', variable: AWS_ACCESS_KEY_ID)], [string(credentialsId: 'aws-secret-access', variable:AWS_SECRET_ACCESS_KEY )]) {
            sh '''
            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
            export AWS_DEFAULT_REGION=us-west-2
        '''
        }
        stages {
            stage('SyntaxTest'){
                steps{
                    sh '''
                        #export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                        #export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
                        #export AWS_DEFAULT_REGION=us-west-2
                        aws cloudformation validate-template --template-body file://vpcStack.yml
                    '''
                }
            }
            stage('Build'){
                steps{
                    sh '''
                        export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                        export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
                        export AWS_DEFAULT_REGION=us-west-2
                        aws cloudformation deploy --stack-name vpcproduccion --template-file vpcStack.yml --capabilities CAPABILITY_NAMED_IAM
                    '''
                }
            }
    }    
    }
    
}