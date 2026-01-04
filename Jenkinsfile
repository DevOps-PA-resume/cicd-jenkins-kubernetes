pipeline {
    agent any

    stages {
        stage('Checkout GitHub repo') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/DevOps-PA-resume/cicd-jenkins-kubernetes']])
            }
        }
        
        stage('Build and Tag Docker Image') {
            steps {
                script {
                    sh 'docker build . -t hellodocker'
                    sh 'docker tag hellodocker therealpad/hellodocker'
                }
            }
        }
        
        stage('Push the Docker Image to DockerHUb') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker_hub', variable: 'docker_hub')]) {
                        sh 'docker login -u therealpad -p ${docker_hub}'
                    }
                    sh 'docker push therealpad/hellodocker'
                }
            }
        }
        
        stage('Deploy deployment and service file') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig_secret_file']) {
                        sh 'kubectl apply -f deploymentsvc.yaml'
                    }
                }
            }
        }
    }
}