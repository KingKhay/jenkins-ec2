pipeline {
    agent any
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/KingKhay/jenkins-ec2.git']])
                sh 'mvn clean install'
            }
        }
    }
}