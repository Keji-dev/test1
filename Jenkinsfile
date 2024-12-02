pipeline {
    agent any  // Esto le dice a Jenkins que ejecute en cualquier agente disponible

    environment {
        DOCKER_IMAGE = 'python:3.9-slim'  // Imagen Docker que usarás
    }

    stages {
        stage('Checkout') {
            steps {
                // Descargar el código fuente desde el repositorio
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Construir la imagen Docker si es necesario
                    // Si ya tienes el contenedor en ejecución, puedes omitir esta parte
                    echo 'No hay necesidad de build, usaremos la imagen directamente.'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Ejecutar pruebas en el contenedor Docker
                    sh """
                    docker run --rm -v \$(pwd):/app:z -w /app $DOCKER_IMAGE bash -c "pip install --no-cache-dir -r requirements.txt && pytest"
                    """
                }
            }
        }
    }

    post {
        always {
            // Limpiar después de ejecutar el pipeline si es necesario
            echo 'Pipeline terminado.'
        }
    }
}
