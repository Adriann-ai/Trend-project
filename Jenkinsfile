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
                         sh 'docker build -t adreann/trend:latest .'
                         sh 'docker push adreann/trend:latest'
                     }
                 }
             }
        }
        stage ('k8s-deploy') {
             steps{
                 withKubeConfig(caCertificate: '', clusterName: 'trend-cluster', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://5FDD14B58FB196B527EE2133BA254924.yl4.ap-south-1.eks.amazonaws.com') {
                 sh "kubectl apply -f manifest/deployment.yaml -n webapps"
                 sh "kubectl apply -f manifest/service.yaml -n webapps"
                 }
             }
        }    
    }
}
