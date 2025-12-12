pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout code from Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        // Use built-in Maven tool named 'MAVEN_3'
                        def mvnHome = tool name: 'MAVEN_3', type: 'maven'
                        env.PATH = "${mvnHome}\\bin;${env.PATH}" // For Windows agents
                        
                        // Run Maven build
                        bat "mvn clean install"
                    } catch (Exception e) {
                        error "Build failed! Maven 'MAVEN_3' is not found or not configured."
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
