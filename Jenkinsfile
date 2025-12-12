pipeline {
    agent any

    environment {
    MAVEN_HOME = tool name: 'Maven 3.9.5', type: 'maven'
    PATH = "${env.MAVEN_HOME}\\bin;${env.PATH}"
}


    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    try {
                        // Checkout from GitHub using credentials
                        checkout([$class: 'GitSCM',
                            branches: [[name: '*/main']],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            userRemoteConfigs: [[
                                url: 'https://github.com/ibrahim-0095/maven-demo.git',
                                credentialsId: 'github-pat'
                            ]]
                        ])
                    } catch (err) {
                        echo "Error during Git checkout: ${err}"
                        error("Checkout failed, stopping the pipeline.")
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        // Run Maven build (Windows uses 'bat' instead of 'sh')
                        bat 'mvn clean install'
                    } catch (err) {
                        echo "Error during build: ${err}"
                        error("Build failed, stopping the pipeline.")
                    }
                }
            }
        }

        stage('Archive Jar') {
            steps {
                script {
                    try {
                        // Archive generated JAR files
                        archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: false
                    } catch (err) {
                        echo "Error during archiving: ${err}"
                        error("Archiving failed.")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the error messages above.'
        }
    }
}

