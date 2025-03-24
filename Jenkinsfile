//1. Global env variable
//2. Environment Variables in Specific Stages
//3. Passing Environment Variables from One Stage to Another
pipeline {
    agent any
    // agent {lable 'Demo'}
    environment{
        registry = "vikas2498"
        Global_Git_URL = "https://github.com/vikas2498/JenkinsFile.git"
        Git_Branch = "main"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    parameters{
        choice(name: 'action', choices: ['Create', 'Delete'], description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'vikas2498')
    }
    stages{
        stage('Git Checkout'){
            when {expression {params.action == 'Create'}}
            steps{
                script{
                    checkout([
                        $class: 'GitSCM',
                        branches:[[name:"*/${env.Git_Branch}"]],
                        userRemoteConfigs: [[url: "${env.Global_Git_URL}"]]
                    ])
                    echo "checking out from ${env.Global_Git_URL} branch ${env.Git_Branch}"
                }
                
            }
        }
        stage('static code analysis: soanrqube'){
            environment{
                Local_ENV_Variable = "local env variable cannot be used outside of the stage"
            }
            when {expression {params.action == 'Create'}}
            steps{
                echo "running static code analysis using sonarqube stage 2 ${Local_ENV_Variable}"
            }

        }
        stage('docker build'){
            when {expression {params.action == 'Create'}}
            steps{
                script{
                   def dockerImage = "${params.ImageName}:${params.ImageTag}"

                   echo "Docker image built in stage 3 is ${dockerImage}"
                }
 
              
            }
        }
        stage ('Push to registry'){
            steps{
                echo "docker image ${env.dockerImage} will be pushed to registry ${env.registry}"
            }
        }
    }
}