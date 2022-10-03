pipeline {
    agent any
    stages {
        stage('Checkout') { 
            steps { 
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/enzopcastillo/demo-nginx']]])
                }
            }
        }
        stage('Build') { 
            steps { 
                script{
                 app = docker.build("enzopcastillo/demo-nginx")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://registry.hub.docker.com/', 'dockerhub_credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}