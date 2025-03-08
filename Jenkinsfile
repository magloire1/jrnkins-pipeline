pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o result.html'
                
                
                
            }
        }
        stage('dockerLoging'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 971422713140.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker build -t jenkins-ci .'
                sh 'docker build -t imageversion .'
            }
        }
        stage('dockerImageTag'){
            steps{
                sh 'docker tag jenkins-ci:latest 971422713140.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
                sh 'docker tag imageversion 971422713140.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:v1.$BUILD_NUMBER'
            }
        }
        stage('pushImage'){
            steps{
                sh 'docker push 971422713140.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
                sh 'docker push 971422713140.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:v1.$BUILD_NUMBER'
            
            }
        }
    }
}