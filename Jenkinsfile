pipeline {
    // Ejecutar el pipeline en cualquier agente disponible
    agent any
    // Variables de entorno para el pipeline
    environment {
        IMAGE_NAME = "flask-vulnerable-app"
    }

    stages {

        stage('Checkout') {

            // Obtener la ultima version del proyecto desde el repositorio git

            steps {
                echo 'Obteniendo código desde Git...'
                checkout scm
            }
        }

        stage('Build') {
            // Instalar las dependencias del proyecto
            steps {
                echo 'Construyendo aplicación...'
                sh 'pip install -r requirements.txt || pip3 install -r requirements.txt'
            }
        }

        stage('Tests') {

            // Verificar que la aplicacion no tenga errores de sintaxis

            steps {
                echo 'Ejecutando pruebas...'
                sh 'python -m py_compile vulnerable_app.py'
            }
        }

        stage('OWASP ZAP') {

            // Aqui se ejecutarán las pruebas con
            // OWASP ZAP para identificar vulnerabilidades
            // en la aplicacion web

            steps {

                echo 'Iniciando analisis de seguridad con OWASP ZAP...'
                // Se agregara el comando de ejecucion
                // una vez configurado OWASP ZAP
                
            }
        }

        stage('Generar Documentación') {

            // Generacion de documentacion
            // utilizando Doxygen para mantener la trazabilidad del proyecto.

            steps {
                echo 'Generando documentación con Doxygen...'
            }
        }

        stage('Docker Build') {

            // Construcción de la imagen Docker 
            // que sera utilizada para desplegar la aplicacion

            steps {
                echo 'Construyendo imagen Docker...'
                sh 'docker build -t ${IMAGE_NAME} .'
            }
        }

        stage('Deploy') {

            // Despliegue de la aplicación Flask mediante un contenedor Docker

            steps {
                echo 'Desplegando aplicación...'
                sh 'docker run -d -p 5000:5000 ${IMAGE_NAME}'
            }
        }
    }
    
}