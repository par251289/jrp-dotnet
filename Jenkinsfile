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
    }
}
