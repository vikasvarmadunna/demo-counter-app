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
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                    }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar'
                    }
                }
            }
    }
}
