pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Reference the NodeJS installation in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo 'Cloning repository...'
                    git credentialsId: 'muthu512', url: 'https://github.com/muthu512/tomcat.git', branch: 'master'
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
                    echo 'Deploying to Tomcat...'
                    def tomcatPath = 'C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\webapps\\ROOT'
                    
                    // Clear the Tomcat webapps ROOT directory
                    bat "del /Q ${tomcatPath}\\*"
                    // Copy the built files to the Tomcat ROOT directory
                    bat "xcopy /S /I /Y build\\* ${tomcatPath}"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployed successfully!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
