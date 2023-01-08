pipeline {
    agent any

    stages{
        stage('git checkout'){
            steps{
                git branch: 'dev', credentialsId: 'java', url: 'https://github.com/vikasvarmadunna/demo-counter-app.git'
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
        stage('maven build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('sonarqube'){
            steps{
                withSonarQubeEnv(credentialsId: 'sonar-api') {
                sh 'mvn clean package sonar:sonar'
}
            }
        }
    }
}
