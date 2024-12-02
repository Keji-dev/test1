pipeline {
    agent any

    environment {
        PYTHON_ENV = "python3"  // Define el intérprete de Python
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar la rama correcta del repositorio
                git branch: 'main', url: 'https://github.com/Keji-dev/test1.git'
            }
        }

        stage('Setup Environment') {
            steps {
                script {
                    // Crear entorno virtual y activarlo
                    sh "${PYTHON_ENV} -m venv venv"
                    sh "./venv/bin/python -m pip install --upgrade pip"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Instalar dependencias
                    sh "./venv/bin/pip freeze > requirements.txt"
                    sh "./venv/bin/pip install -r requirements.txt"
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Ejecutar pruebas con reporte compatible con Jenkins
                    sh "./venv/bin/pytest --junitxml=results.xml"
                }
            }
        }
    }

    post {
        always {
            // Publicar reportes de pruebas
            junit 'results.xml'

            // Limpiar el entorno virtual
            sh 'rm -rf venv'
        }
    }
}
