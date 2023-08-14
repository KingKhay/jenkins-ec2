pipeline {
    agent {
        docker {
            image 'maven:3.8' // Specify the Docker image you want to use
            args '-v $HOME/.m2:/root/.m2' // Mount Maven cache to avoid downloading dependencies on every build
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install' // Execute Maven build command inside the Docker container
            }
        }

        stage('Test'){
            steps {
                sh 'mvn test' // Run Maven test inside the Docker container
            }
        }
    }
}