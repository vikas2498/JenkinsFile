pipeline{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
    }
    environment {
        APP_NAME = "My-Web-APP"
        APP-VERSION = "V1.0"
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/vikas2498/JenkinsFile.git'
                echo "Git Checkout satge 1"
            }
        }

        stage ('Unit Tes'){
            steps{
                echo "Unit testing stage 2"
            }
        }

        stage ('Integration Test'){
            steps{
                echo "Integration testing stage 3"
            }
        }

        stage('Static code analysis: Snarqube'){
            steps{
                echo "Static code analysis stage 4"
            }
        }

        stage('Quality gate status check: Sonarqube'){
            steps{
                echo "Quality gate status check stage 5"
            }
        }

        stage('build'){
            steps{
                echo "binary build stage 6"
            }
        }

        stage('Deploy'){
            steps{
                echo "Deploy stage 7"
            }
        }


    }
}