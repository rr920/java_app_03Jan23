@Library('Jenkins_Shared_Lib') _

pipeline{

    agent any

    stages{
        stage('Git Checkout'){

            steps{
                script{
                    git 'https://github.com/rr920/java_app_02Jan23.git'
                }
            }
        }

        stage('Unit Test Maven'){

            steps{
                script{
                    'mvn test'
                }
            }
        }
        stage('Maven Integration Test'){

            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
    }
}