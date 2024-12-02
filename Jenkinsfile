pipeline {
    agent any

    environment {
        IMAGE_NAME = 'python:3.9-slim'
        WORKSPACE = '/var/jenkins_home/workspace/test1'
        DOCKER_TOOL = 'docker' // Aquí defines el nombre del Docker Tool que has configurado
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Keji-dev/test1.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "No hay necesidad de build, usaremos la imagen directamente."
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.withTool(DOCKER_TOOL) { // Usa dockerTool si es necesario
                        docker.image(IMAGE_NAME).inside {
                            sh 'pip install --no-cache-dir -r requirements.txt'
                            sh 'pytest'
                        }
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
            cleanWs()
        }
    }
}
