pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git url: 'https://github.com/carlosdelgadillo10/suma_windows.git', branch: 'main'
            }
        }
        stage('Setup Python Environment') {
            steps {
                script {
                    // Instalación de dependencias en un entorno virtual
                    sh 'python3 -m venv venv'
                    sh './venv/bin/pip install -r requirements.txt'
                }
            }
        }
    }
}
