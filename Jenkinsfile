pipeline {
    agent any 

    stages {
        stage('Deploy to K8s') {
            agent {
                // ใช้ image ที่มี kubectl เตรียมไว้ให้แล้ว
                docker { 
                    image 'bitnami/kubectl:latest'
                    // ถ้าใช้กับ cluster ภายนอกต้องส่ง config เข้าไปด้วย
                    args '-v $HOME/.kube:/root/.kube' 
                }
            }
            steps {
                script {
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