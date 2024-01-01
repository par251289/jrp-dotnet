pipeline {
    agent any

    stages {
        stage ('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage ('Git Checkout'){
             steps {
                git branch: 'main', credentialsId: '3d01c375-b5a7-4ea5-b3dd-f78154320e1c', url: 'git@github.com:par251289/jrp-dotnet.git'
             }
        }

        stage ('Restore packages') {
            steps {
                sh "dotnet restore ${workspace}/src/NopCommerce.sln"
            }
        }

        stage ('Build Packages') {
            steps {
                sh "dotnet build ${workspace}/src/NopCommerce.sln"
            }
        }

        stage ('Build Docker image') {
            steps {
                withAWS(credentials: '215915c3-b15e-4292-b5f0-88df80563460', region: 'us-east-1') {
                    sh "aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/e3b1m7f3"
                    sh "docker build -t dotnet ."
                    sh "docker tag dotnet:latest public.ecr.aws/e3b1m7f3/dotnet:latest"
                    sh "docker push public.ecr.aws/e3b1m7f3/dotnet:latest"
                }
                  
            }
        }
    }
}
