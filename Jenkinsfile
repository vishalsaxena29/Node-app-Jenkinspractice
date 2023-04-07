 pipeline {
    agent any 
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages {
        stage ("Build Docker Image"){//In this stage we are building the Docker image using the Cloned app files from git from our workspace folder
            steps{
                sh "docker build . -t vishalsaxena29/nodeapp:${DOCKER_TAG}"
            }
        }
        stage("DockerHub Push"){ //In this stage will push the build image to Docker Hub 
            steps{
                withCredentials([string(credentialsId: 'DockerHubPass', variable: 'DockerHubPwd')]) {
                        sh "docker login -u vishalsaxena29 -p ${DockerHubPwd}"
                        sh "docker push vishalsaxena29/nodeapp:${DOCKER_TAG}"
                    }  
            }
        }

    }
 }

 def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
 }