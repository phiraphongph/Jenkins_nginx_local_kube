pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // สมมติว่าเก็บไฟล์ไว้ใน Git
                checkout scm
            }
        }

        stage('Deploy to K8s') {
            steps {
                script {
                    // ใช้คำสั่ง kubectl apply เพื่อ deploy nginx
                    sh 'kubectl apply -f nginx-deployment.yaml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl get pods'
                sh 'kubectl get service'
            }
        }
    }
}