	pipeline {
    agent any

    environment{
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }

    stages {
        stage('git') {
            steps {
                git branch: 'main' , url: 'https://github.com/UmangKhandelwal23/IntellipatPRT2025'
            }
        }
        stage('dockerbuild') {
            steps {
                sh 'docker build -t umangkhandelwal/intellipat2025:v2 ${WORKSPACE}'
                sh 'docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'docker push umangkhandelwal/intellipat2025:v2'
            }
        }
        
        stage('K8') {
            steps {
                export KUBECONFIG=/var/lib/jenkins/.kube/config
                sh 'kubectl apply -f Deployment.yml'
                sh 'kubectl apply -f Service.yml'
            }
        }
    }
}

