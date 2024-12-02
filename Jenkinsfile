pipeline {
    agent any

    environment {
        PYTHON_ENV = "python3"  // Usa el intérprete de Python que prefieras
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar la rama correcta del repositorio
                git branch: 'main', url: 'https://github.com/Keji-dev/test1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                    #!/bin/bash
                    python3 -m venv venv
                    source venv/bin/activate
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
