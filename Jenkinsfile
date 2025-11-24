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
                         sh 'docker build -t adrian0186/trend-project:latest .'
                         sh 'docker push adrian0186/trend-project:latest'
                     }
                 }
             }
        }
        stage ('k8') {
             steps{
                 withKubeConfig(caCertificate: '', clusterName: 'my-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://F233AB1DE84E5B6B8593CD15900C14FB.gr7.ap-south-1.eks.amazonaws.com') {
                 sh "kubectl apply -f manifest/deployment.yaml -n webapps"
                 }
             }
        }    
    }
}