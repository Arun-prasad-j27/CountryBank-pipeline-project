pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Arun-prasad-j27/CountryBank-pipeline-project.git'
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments:'--scan ./',odcInstallation:'DC'
                    dependencyCheckPublisher pattern:'**/dependency-check-report.xml' 
            }
        }
        
        stage('Trivy ') {
            steps {
                sh "trivy fs ."
            }
        }
        
        stage('Docker Build & Deploy') {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
