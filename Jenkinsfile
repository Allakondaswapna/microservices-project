pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh '''
                    aws eks update-kubeconfig --region ap-south-1 --name EKS-1
                    kubectl apply -f deployment-service.yml -n webapps
                    '''
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh '''
                    aws eks update-kubeconfig --region ap-south-1 --name EKS-1
                    kubectl get svc -n webapps
                    '''
                }
            }
        }
    }
}
