pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Reference to NodeJS installation
    }

    environment {
        TOMCAT_PATH = "C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\webapps\\ROOT"
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo 'Cloning repository...'
                    git credentialsId: 'muthu512', url: 'https://github.com/muthu512/tomcat.git'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    bat 'npm install'
                }
            }
        }
        stage('Build React App') {
            steps {
                script {
                    echo 'Building React app...'
                    bat 'npm run build'
                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                script {
                    echo "Deploying to Tomcat at ${TOMCAT_PATH}..."
                    // Clean existing files in ROOT directory
                    bat "del /Q ${TOMCAT_PATH}\\*"

                    // Copy new build files to Tomcat's ROOT directory
                    bat "xcopy /S /I /Y build\\* ${TOMCAT_PATH}\\"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
