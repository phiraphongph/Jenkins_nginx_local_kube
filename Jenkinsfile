pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            steps {
                // ใช้กุญแจ kubeconfig-file ที่เราแก้ ID แล้ว
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    script {
                        // ใช้ kubectl ที่เราติดตั้งไว้ในตัว Jenkins (ตามวิธีที่ผมบอกก่อนหน้านี้)
                        sh 'kubectl apply -f nginx-deployment.yaml'
                    }
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    sh 'kubectl get pods'
                    sh 'kubectl get service'
                }
            }
        }
    }
}