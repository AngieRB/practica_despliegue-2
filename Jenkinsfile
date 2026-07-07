pipeline {
    agent any

    tools {
        nodejs "Node22"
        dockerTool 'Dockertool' 
    }

    stages {
        stage('Construir Imagen Docker') {
            steps {
                sh '''
                # Usamos la ruta absoluta directa al binario de Docker
                /var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool/docker/docker build -t hola-mundo-node:latest .
                '''
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                # Usamos la ruta absoluta para detener, eliminar y correr
                /var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool/docker/docker stop hola-mundo-node || true
                /var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool/docker/docker rm hola-mundo-node || true
                
                /var/jenkins_home/tools/org.jenkinsci.plugins.docker.commons.tools.DockerTool/Dockertool/docker/docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}