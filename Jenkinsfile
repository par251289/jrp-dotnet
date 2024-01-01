pipeline {
    agent any

    stages {
        stage ('Clean Workspace') {
            steps {
                cleans()
            }
        }

        stage ('Git Checkout'){
             steps {
                git branch: 'master', credentialsId: '3d01c375-b5a7-4ea5-b3dd-f78154320e1c', url: 'git@github.com:par251289/jrp-dotnet.git'
             }
        }
    }
}
