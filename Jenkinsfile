pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/yourrepo.git'
            }
        }
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner' // Set this to your scanner name
            }
            steps {
                withSonarQubeEnv('My SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=your_project_key -Dsonar.projectName='Your Project Name'"
                }
            }
        }
        stage('Build') {
            steps {
                // your build commands, e.g., Maven, Gradle, npm, etc.
            }
        }
    }
}
