pipeline {
    agent any
    environment {
        AWS_REGION = 'ap-southeast-2'
        AWS_ACCOUNT_ID = '951066974787'
        IMAGE_TAG = 'latest'
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Using the GitHub credentials ID created above
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/anupam66kumar/SampleMERNwithMicroservices.git', 
                    credentialsId: 'github-anupam-pat-credentials']]
                ])
            }
        }
        stage('Build and Push Services') {
            steps {
                script {
                    // Injecting AWS credentials securely for the ECR login & push session
                    withCredentials([aws(credentialsId: 'aws-anupam-ecr-credentials', 
                                         accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                                         secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        
                        // Authenticate Docker to ECR
                        sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
                        
                        // Build and Push Hello Service
                        def helloImg = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/helloservice:${IMAGE_TAG}", "./helloservice")
                        helloImg.push()

                        // Build and Push Profile Service
                        def profileImg = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/profileservice:${IMAGE_TAG}", "./profileservice")
                        profileImg.push()

                        // Build and Push Frontend
                        def frontendImg = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/frontend:${IMAGE_TAG}", "./frontend")
                        frontendImg.push()
                    }
                }
            }
        }
    }
}
