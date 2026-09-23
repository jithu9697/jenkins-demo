pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: jenkins
  containers:
  - name: kubectl
    image: bitnami/kubectl:latest
    command: ["sleep"]
    args: ["99d"]
'''
        }
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Deploy') {
            steps {
                container('kubectl') {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
    post {
        success { echo 'Deployed successfully!' }
    }
}
