pipeline{
    agent any 
    tools {
        go 'GO-1.20.2'
    }

    environment {
        GO111MODULE='on'
    }
    stages{
        stage('test'){
            steps{
                git 'https://github.com/hemant-sw/go-webapp-sample.git'
                sh 'go test ./...'
            }
        }
    }
}