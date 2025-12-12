pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        def mvnHome = tool name: 'Maven 3', type: 'maven' // Use exact name from Jenkins
                        env.PATH = "${mvnHome}\\bin;${env.PATH}"         // Windows path
                        bat "mvn clean install"
                    } catch (Exception e) {
                        error "Build failed! Check your Maven installation or compilation errors."
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed! Check the error messages above."
        }
        success {
            echo "Pipeline succeeded!"
        }
    }
}
