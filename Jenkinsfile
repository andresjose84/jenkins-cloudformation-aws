pipeline {
    agent any

    environment {
        STACK_NAME = 'my-cloudformation-stack'
        TEMPLATE_FILE = 'template.yaml'
        AWS_REGION = 'us-east-2'
        AWS_ACCESS_KEY_ID = credentials('aws-credential-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-credential-id')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Template') {
            steps {
                script {
                    sh "aws cloudformation validate-template --template-body file://${TEMPLATE_FILE}"
                }
            }
        }

        stage('Deploy Stack') {
            steps {
                script {
                    sh """
                        aws cloudformation deploy \
                        --template-file ${TEMPLATE_FILE} \
                        --stack-name ${STACK_NAME} \
                        --region ${AWS_REGION} \
                        --capabilities CAPABILITY_NAMED_IAM
                    """
                }
            }
        }
    }
}