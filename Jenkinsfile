pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    script {
                        // เพิ่ม flag --insecure-skip-tls-verify ไว้ท้ายสุด
                        sh 'kubectl apply -f nginx-deployment.yaml --insecure-skip-tls-verify'
                    }
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    sh 'kubectl get pods --insecure-skip-tls-verify'
                    sh 'kubectl get service --insecure-skip-tls-verify'
                }
            }
        }
    }
}