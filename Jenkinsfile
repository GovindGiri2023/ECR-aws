
pipeline {
    environment {
    registry = 'gallery.ecr.aws/u2n5m5v5/govind-aws-ecr'
    registryCredential = 'Aws-access-for-ECR'
    dockerImage = ''
    }
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                    app = docker.build("demoimage:${env.BUILD_ID}")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{ 
                        docker.withRegistry("https://" + registry, "ecr:us-east-1:" + registryCredential) {
                        app.push()
                    }
                }
            }
        }
    }
}
