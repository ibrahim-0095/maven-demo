pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/YOUR_USERNAME/maven_demo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Jar') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}

