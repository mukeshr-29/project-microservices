pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'microservice', contextName: '', credentialsId: 'k8s', namespace: 'webapps', serverUrl: 'https://258BE6BFCE91F8570077D96F42390DDC.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'microservice', contextName: '', credentialsId: 'k8s', namespace: 'webapps', serverUrl: 'https://258BE6BFCE91F8570077D96F42390DDC.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
