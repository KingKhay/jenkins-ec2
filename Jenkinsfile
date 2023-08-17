pipeline {
    agent any
    tools {
        maven 'Maven_3'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KingKhay/jenkins-ec2.git']])
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image'){
            steps {
               sh "docker build -t khaydev1/jenkins-ec2:1.0.${env.BUILD_ID} ."
            }
        }
        stage('Push Docker Image'){
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhub-pwd')]) {
                        sh "docker login -u khaydev1 -p ${dockerhub-pwd}"
                    }
                    sh "docker push khaydev1/jenkins-ec2:1.0.${env.BUILD_ID}"
                }
            }
        }
    }
}