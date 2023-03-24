#!/usr/bin/env groovy

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                     sh 'mvn clean package'
                }
            }
        }
        
        
//         stage('test') {
//             steps {
//                 script {
//                     echo "Testing the application..."
//                 }
//             }
//         }
        stage('deploy') {
            steps {
                script {
                    docker.withRegistry('https://524395221959.dkr.ecr.eu-north-1.amazonaws.com', 'ecr:eu-north-1:aws-credentials') {
                    sh "docker build -t my-app ."
                    sh "docker tag my-app 524395221959.dkr.ecr.eu-north-1.amazonaws.com/my-app:1.0"
                    // push image
                    sh "docker push 524395221959.dkr.ecr.eu-north-1.amazonaws.com/my-app:1.0"
                    }
                }
            }
        }
    }
}
