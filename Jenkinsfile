pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: alpine:latest
    command: ["sleep"]
    args: ["99d"]
'''
        }
    }
    stages {
        stage('Checkout Confirm') {
            steps {
                container('shell') {
                    sh 'ls -la && cat hello.txt'
                }
            }
        }
    }
}
