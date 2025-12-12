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
                        // Use the Maven installation configured in Jenkins
                        def mvnHome = tool name: 'MAVEN_3', type: 'maven'
                        env.PATH = "${mvnHome}\\bin;${env.PATH}"

                        // Run Maven build on Windows
                        bat "mvn clean package"

                        // Archive the generated .jar file
                        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true

                    } catch (Exception e) {
                        error "Build failed! Check your Maven installation or compilation errors."
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! .jar archived successfully."
        }
        failure {
            echo "Pipeline failed! Check the error messages above."
        }
    }
}
