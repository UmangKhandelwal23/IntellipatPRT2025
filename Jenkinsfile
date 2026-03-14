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
                sh 'sudo docker build -t umangkhandelwal/intellipat2025:v1 ${WORKSPACE}'
                sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'
                sh 'sudo docker push umangkhandelwal/intellipat2025:v1'
            }
        }
        
        stage('K8') {
            steps {
                sh 'sudo kubectl apply -f Deployment.yml'
                sh 'sudo kubectl apply -f Service.yml'
            }
        }
    }
}

