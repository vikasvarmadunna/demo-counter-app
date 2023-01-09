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
                    
                    withSonarQubeEnv(credentialsId: 'sonar-apis') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                }
                    
                }
            }
        stage('quality gate analysis'){
            
            steps{
                
                script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-apis'
                }
            }
        }
        stage('nexus repository'){
            
            steps{
                
                script{
                        
                        nexusArtifactUploader artifacts:
                        [
                            [
                                artifactId: 'springboot',
                                classifier: '', file: 'target/Uber.jar',
                                type: 'jar'
                                ]
                        ],     
                        credentialsId: 'vyshu',
                        groupId: 'com.example', 
                        nexusUrl: '44.211.37.12:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http',
                        repository: 'demoapp-release',
                        version: '1.0.0'
                }
            }
        }

    }
}


