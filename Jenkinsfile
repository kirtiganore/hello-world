pipeline {
    agent any
    environment {
        // Set environment variables
        SONARQUBE_SERVER = 'sonar-kirti-project' // Name of your SonarQube server configuration in Jenkins
        MAVEN_TOOL = 'Maven 3.8' // Name of your Maven tool in Jenkins global tools
        SONAR_TOKEN = 'sqp_5a895e0b86b84489346eb1c8c783a80731da488a' // Your SonarQube token
    }
    stages {
        stage('Checkout') {
            steps {
                // Replace with your actual repo URL
                git branch: 'main', url: 'https://github.com/kirtiganore/hello-world.git'
            }
        }
        stage('SonarQube Scan') {
            steps {
                // Run Maven with SonarQube analysis
                script {
                    def mavenHome = tool MAVEN_TOOL
                    withSonarQubeEnv(SONARQUBE_SERVER) {
                        sh "${mavenHome}/bin/mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=kirti-maven \
                            -Dsonar.projectName=kirti-maven \
                            -Dsonar.host.url=http://54.206.8.166:9000 \
                            -Dsonar.login=${SONARQUBE_TOKEN}"
                    }
                }
            }
        }
    }
}
