pipeline {
    agent any

    environment {
        PYTHON_ENV = "python3"  // Usa el intérprete de Python que prefieras
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar el repositorio
                git 'https://github.com/Keji-dev/test1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Instalar las dependencias desde requirements.txt
                script {
                    sh '''
                    # Crear un entorno virtual y activarlo
                    python3 -m venv venv
                    source venv/bin/activate
                    # Instalar las dependencias
                    pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Ejecutar las pruebas usando pytest
                script {
                    sh '''
                    source venv/bin/activate
                    pytest test_main.py
                    '''
                }
            }
        }
    }

    post {
        always {
            // Limpiar el entorno virtual
            sh 'rm -rf venv'
        }
    }
}
