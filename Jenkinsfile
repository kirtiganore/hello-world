pipeline {

    agent any



    environment {

        MAVEN_HOME = '/usr/share/maven' // Path to Maven installation

        SONARQUBE_SERVER = 'SonarQube'  // SonarQube server configured in Jenkins

        NEXUS_REPO = 'http://nexus.example.com/repository/maven-releases/' // Nexus repository URL

    }



    stages {

        stage('Checkout Code') { // Clones the repository

            steps {

                git 'https://github.com/your-repo/java-app.git'

            }

        }



        stage('Build with Maven') { // Builds the project and creates JAR/WAR

            steps {

                sh 'mvn clean package'

            }

        }



        stage('Run Unit Tests') { // Executes unit tests

            steps {

                sh 'mvn test'

            }

        }



        stage('Code Analysis with SonarQube') { // Runs static code analysis

            steps {

                withSonarQubeEnv(SONARQUBE_SERVER) {

                    sh 'mvn sonar:sonar'

                }

            }

        }



        stage('Publish to Nexus') { // Uploads artifact to Nexus repository

            steps {

                sh 'mvn deploy -DaltDeploymentRepository=nexus-releases::default::${NEXUS_REPO}'

            }

        }



        stage('Deploy to Test Server') { // Deploys JAR to a remote server

            steps {

                sh 'scp target/*.jar user@your-server:/opt/app/' // Copies JAR

                sh 'ssh user@your-server "systemctl restart java-app"' // Restarts app

            }

        }

    }



    post {

        success {

            echo 'Build and deployment successful!'

        }

        failure {

            echo 'Build failed!'

        }

    }

}
