pipeline {
    agent none
    stages {
        stage('Build Dev') {
            agent {
                label {
                    label 'dev'
                    customworkspace "/opt/go-app"
                }
            }
            steps {
                sh 'git pull'

            }
        }
        stage('Test Dev ') {
            agent {
                label {
                    label 'dev'
                    customworkspace "/opt/go-app"

                }
            }
            sh 'go test ./...'
        }
    }
    stage('Deploy  Dev ') {
        agent {
            label {
                label 'dev'
                customworkspace "/opt/go-app"

            }
        }
        steps {
            script {
                withEnv ( [ 'JENKINS_NODE_COOKIE=do_not_kill'] ) {
                    sh 'go run main.go &'
                }
            }
        }
    }
    stage ('Build Prod') {
        agent {
            label  {
                label 'prod'
                customworkspace "/opt/go-app"
            }
        }
        steps {
            sh 'git pull'

        }
    }
    stage('Test Prod') {
        agent {
            label {
                 label 'prod'
                 customworkspace "/opt/go-app"
            }
        }
        steps {
                sh 'go test ./...'
            }
        }
        stage('Deploy Prod') {
            agent {
              label {
                label 'prod'
                customWorkspace "/opt/go-app"
              }
            }
            steps {
              script {
                withEnv ( ['JENKINS_NODE_COOKIE=do_not_kill'] ) {
                  sh 'go run main.go &'
                  }
                }
            }
        }
    }
