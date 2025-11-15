pipeline{
    agent any
    stages{
        stage ('git checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Adriann-ai/Trend-project.git'
            }
        }
        stage ('docker build and push to hub') {
             steps{
                 script{
                     withDockerRegistry(credentialsId: 'dockerhub-cred') {
                         sh 'docker build -t adrian0186/testpro:latest .'
                         sh 'docker push adrian0186/testpro:latest'
                     }
                 }
             }
        }
    }
}