pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }

    stages {
        stage('build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
