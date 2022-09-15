
pipeline {
    environment {
    registry = '603540392829.dkr.ecr.us-east-1.amazonaws.com/govind-aws-registry'
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
                    app = docker.build("govind-aws-registry:${env.BUILD_ID}")
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
                        app.push(ubuntu)
                    }
                }
            }
        }
    }
}
