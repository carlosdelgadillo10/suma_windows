def app
pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build image') {
            steps {
                script {
                    // Construir imagen Docker
                    app = docker.build("carlosdelgadillo/suma_windows")
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    sh ("docker run -d -p 8001:8001 carlosdelgadillo/suma_windows:${BUILD_NUMBER}")
                }
            }
        }
        
    }
        

   
}

