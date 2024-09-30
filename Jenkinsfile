pipeline {
    agent any

    environment {
        // Replace with your SonarQube server configuration name in Jenkins
        SONARQUBE_SERVER = 'Sonarqube'  
        // Optional: Define the Git branch to build
        GIT_BRANCH = 'main'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone your GitLab repository (replace with your repository URL)
                git branch: "${GIT_BRANCH}", url: 'https://gitlab.com/your_username/your_repo.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube Scanner for static code analysis
                script {
                    withSonarQubeEnv(SONARQUBE_SERVER) {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=project-2 -Dsonar.host.url=${http://localhost:9000} -Dsonar.login=${sqp_0c421f5e4c9a64f6df0be40eb8b39340a04225cf}'
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                // Build your Java application (assuming Maven is used)
                sh 'mvn clean install'
            }
        }
    }

    post {
        always {
            // Archive any build artifacts (optional)
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            // Collect test results (optional)
            junit '**/target/surefire-reports/*.xml'
        }

        success {
            echo 'Build and SonarQube analysis completed successfully!'
        }

        failure {
            echo 'Build or SonarQube analysis failed!'
        }
    }
}
