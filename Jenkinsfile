pipeline {
    agent any

    stages {
        stage('clone the project') {
            steps {
                git branch: 'feature/2025.10.20', credentialsId: 'githubcredentials', url: 'https://github.com/ramya05123/onlinebookstore.git'
            }
        }
        stage('build the project') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('tests') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Artifact publisher') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }
        stage('Deploy to Tomcat server') {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatcredentials', path: '', url: 'http://localhost:8080/')], contextPath: 'ramyaAWSandDevops', war: 'target/*.war'
            }
        }
    }
}
