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
        stage ('k8s') {
             steps{
                 withKubeConfig(caCertificate: '', clusterName: 'my-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://174F91A4766F16CD59A10CA82670448A.gr7.ap-south-1.eks.amazonaws.com') {
                 sh "kubectl apply -f dist/manifest/deployment.yaml -n webapps"
                 }
             }
        }    
    }
}