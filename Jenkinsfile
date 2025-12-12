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
                        // Use the exact Maven installation name
                        def mvnHome = tool name: 'MAVEN_3', type: 'maven'
                        env.PATH = "${mvnHome}\\bin;${env.PATH}"
                        
                        // Run Maven build on Windows
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
