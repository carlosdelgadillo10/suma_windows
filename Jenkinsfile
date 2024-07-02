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
                    // Uso de 'bat' para comandos de Windows
                    bat '''
                        python -m venv venv
                        call venv\\Scripts\\activate
                        pip install -r requirements.txt
                    '''
                }
            }
        }
    }
}
