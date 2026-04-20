pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            agent {
                docker { 
                    image 'bitnami/kubectl:latest'
                    args '--entrypoint=""' 
                }
            }
            steps {
                // ดึงไฟล์ที่เราอัปโหลดเข้าไปมาใช้งาน
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    script {
                        // kubectl จะใช้ไฟล์จากตัวแปร KUBECONFIG อัตโนมัติ
                        sh 'kubectl apply -f nginx-deployment.yaml'
                    }
                }
            }
        }

        stage('Verify Deployment') {
            agent {
                docker { image 'bitnami/kubectl:latest'; args '--entrypoint=""' }
            }
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
                    sh 'kubectl get pods'
                    sh 'kubectl get service'
                }
            }
        }
    }
}