pipeline {
    agent any

    tools {
        nodejs "Node25" // Configura una instalación de Node.js en Jenkins
        dockerTool 'Dockertool' // Herramienta de Docker configurada en Jenkins
    }

    stages {
        stage('Construir Imagen Docker') {
            steps {
                sh '''
                # Le decimos a la terminal dónde encontrar el comando docker descargado
                export PATH=$PATH:/var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool
                
                # Construimos la imagen
                docker build -t hola-mundo-node:latest .
                '''
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                # Exportamos nuevamente la ruta para esta etapa
                export PATH=$PATH:/var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool
                
                # Detener y eliminar cualquier contenedor previo para evitar conflictos
                docker stop hola-mundo-node || true
                docker rm hola-mundo-node || true
                
                # Ejecutar el contenedor de la aplicación
                docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}