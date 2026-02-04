#!/usr/bin.env groovy
library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://gitlab.com/twn-devops-bootcamp/latest/09-aws/jenkins-shared-library.git',
    credentialsID: 'gitlab-credentials'
    ]
)


pipeline {   
    agent any
    tools {
        maven 'Maven'
    }
    environment {
        IMAGE_NAME = ''
    }
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."

                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building the application..." 
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    // def dockerCmd = 'docker run -p 3080:3080 -d marvinggg/demo-app:1.0'
                    def dockerComposeCmd = "docker-compose -f docker-compose.yaml up --detach"
                    sshagent (['ec2-server-key']) {
                        sh "scp docker-compose.yaml ec2-user@18.184.54.160:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@3.138.103.69 ${dockerComposeCmd}"
                    }
                }
            }
        }               
    }
} 
