pipeline {
    agent any
    
    environment {
        // Define variables de entorno que puedan ser reutilizadas
        IMAGE_NAME = 'python:3.9-slim'  // Imagen de Docker a utilizar
        WORKSPACE = '/var/jenkins_home/workspace/test1'  // Ruta del workspace en Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Hacer checkout desde el repositorio Git
                git url: 'https://github.com/Keji-dev/test1.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Ejecutar los pasos de build si es necesario, aquí no es necesario
                    echo "No hay necesidad de build, usaremos la imagen directamente."
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Usar Docker para ejecutar los comandos en el contenedor
                    docker.image(IMAGE_NAME).inside {
                        // Ejecutar los comandos dentro del contenedor Docker
                        sh 'pip install --no-cache-dir -r requirements.txt'  // Instalar dependencias
                        sh 'pytest'  // Ejecutar las pruebas
                    }
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Pipeline terminado.'
            }
        }
    }

    post {
        always {
            // Este bloque se ejecutará siempre, incluso si el pipeline falla
            cleanWs()  // Limpiar el workspace de Jenkins
        }
    }
}
