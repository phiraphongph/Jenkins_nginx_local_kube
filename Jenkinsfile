pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            agent {
                docker { 
                    image 'bitnami/kubectl:latest'
                    args '--entrypoint="" -v $HOME/.kube:/root/.kube' 
                }
            }
            steps {
                script {
                    // 1. เช็กว่าไฟล์เข้ามารึยัง
                    sh 'ls -la /root/.kube'
                    // 2. เช็กว่า kubectl เห็น cluster ไหนอยู่
                    sh 'kubectl config view'
                    // 3. รันคำสั่งจริง
                    sh 'kubectl apply -f nginx-deployment.yaml'
                }
            }
        }

        stage('Verify Deployment') {
            agent { docker { image 'bitnami/kubectl:latest'; args '-v $HOME/.kube:/root/.kube' } }
            steps {
                sh 'kubectl get pods'
                sh 'kubectl get service'
            }
        }
    }
}