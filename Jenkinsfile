pipeline {
    agent any

    stages{
        stage('git checkout'){
            steps{
                git branch: 'dev', credentialsId: 'vyshu', url: 'https://github.com/vikasvarmadunna/demo-counter-app.git'
            }
        }
        stage('unit testing'){
            steps{
                sh 'mvn test'
            }
        }
        stage('integration testing'){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
    }
}