pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: node
    image: node:20-alpine
    command: ["sleep"]
    args: ["99d"]
'''
        }
    }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Install') {
            steps { container('node') { sh 'npm install' } }
        }
        stage('Test') {
            steps { container('node') { sh 'npm test' } }
        }
    }
    post {
        success { echo 'Build and tests passed!' }
        failure { echo 'Build failed — check logs.' }
    }
}
