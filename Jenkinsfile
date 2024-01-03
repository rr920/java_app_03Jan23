@Library('Jenkins_Shared_Lib') _

pipeline{

    agent any

    parameters{
    
        choice(name: 'action', choices: 'create\ndelete', description: 'Choice create/Destroy')
    }

    stages{
        
        stage('Git Checkout'){
        when {expression { params.action == 'create'}}
            steps{
                script{
                    git 'https://github.com/rr920/java_app_02Jan23.git'
                }
            }
        }

        stage('Unit Test Maven'){
        when {expression { params.action == 'create'}}
            steps{
                script{
                    'mvn test'
                }
            }
        }
        stage('Maven Integration Test'){
        when {expression { params.action == 'create'}}
            steps{
                script{
                    'mvn verify -DskipUnitTests'
                }    
            }
        }

        stage('Static code analysis: Sonarqube'){
        when {expression { params.action == 'create'}}
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'sonarqube-api') {    
                    'mvn clean package sonar:sonar'
                }
            
                }    
            }
        }

        stage('Quality Gate Status Check: Sonarqube'){
        when {expression { params.action == 'create'}}
            steps{
                script{
                    'waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-api''  
                   
            
                }    
            }
        }
    }
}