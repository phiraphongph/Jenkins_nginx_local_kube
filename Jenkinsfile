pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    script {
                        // เพิ่ม --validate=false เพื่อข้ามการเช็ก OpenAPI ที่มักจะติดเรื่อง Network
                        sh 'kubectl apply -f nginx-deployment.yaml --insecure-skip-tls-verify --validate=false'
                    }
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    // เพิ่ม flag เดียวกันในทุกคำสั่ง
                    sh 'kubectl get pods --insecure-skip-tls-verify'
                }
            }
        }
    }
}