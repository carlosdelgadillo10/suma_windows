pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    // Instalación de dependencias en un entorno virtual en Windows
                    bat '''
                        python -m venv venv
                        call venv\\Scripts\\activate
                        pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests and Coverage') {
            steps {
                script {
                    // Ejecutar pruebas y cobertura con pytest en Windows
                    bat '''
                        call venv\\Scripts\\activate
                        set PYTHONPATH=%CD%
                        pytest --cov=app --cov-report=xml:coverage.xml --cov-report=term-missing --junit-xml=pytest-report.xml
                    '''
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SCANNER_HOME = tool 'sonar-scanner'
            }
            steps {
                script {
                    // Ejecución de análisis SonarQube en Windows
                    withSonarQubeEnv('server-sonar') {
                        bat """
                            "%SCANNER_HOME%\\bin\\sonar-scanner" ^
                            -Dsonar.projectKey=suma-fastapi ^
                            -Dsonar.projectName='Mi Proyecto Python' ^
                            -Dsonar.sources=app ^
                            -Dsonar.tests=tests ^
                            -Dsonar.sourceEncoding=UTF-8 ^
                            -Dsonar.python.coverage.reportPaths=coverage.xml ^
                            -Dsonar.projectVersion=${env.BUILD_NUMBER}
                        """
                    }
                }
            }
        }
    }

    post {
        always {
            // Limpieza después de la ejecución
            bat 'rmdir /s /q venv'
        }
    }
}
