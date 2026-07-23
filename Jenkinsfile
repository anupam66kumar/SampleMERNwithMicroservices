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
                checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/anupam66kumar/SampleMERNwithMicroservices.git', 
                    credentialsId: 'anupam-github-pat']]
                ])
            }
        }
        stage('Build and Push Services') {
            steps {
                script {
                    withCredentials([aws(credentialsId: 'aws-ecr-credentials', 
                                         accessKeyVariable: 'AWS_ACCESS_KEY_ID', 
                                         secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        
                        // Authenticate Docker to ECR
                        sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
                        
                        // Build and Push Hello Service (inside backend folder)
                        def helloImg = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/helloservice:${IMAGE_TAG}", "./backend/helloService")
                        helloImg.push()

                        // Build and Push Profile Service (inside backend folder)
                        def profileImg = docker.build("${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/profileservice:${IMAGE_TAG}", "./backend/profileService")
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
