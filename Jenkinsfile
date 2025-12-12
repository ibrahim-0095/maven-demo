pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
    }

    stages {

        stage('Checkout') {
    steps {
        git(
            url: 'https://github.com/ibrahim-0095/maven-demo.git',
            branch: 'main',
            credentialsId: 'github-pat'
        )
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



