pipeline {
    agent any
    tools {
        maven 'Maven_3'
    }
    environment {
        dockerHubCredentials = 'dockerhub-login'
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
               withDockerRegistry(credentialsId: dockerHubCredentials, url: 'https://registry.hub.docker.com') {
                   sh "docker build -t khaydev1/jenkins-ec2:1.0.${env.BUILD_ID} ."
                   sh "docker push khaydev1/jenkins-ec2:1.0.${env.BUILD_ID}"
               }
            }
        }
    }
}