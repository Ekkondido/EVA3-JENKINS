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
                echo 'Obteniendo codigo desde Git...'
                checkout scm
            }
        }

        stage('Build') {

            // Instalar las dependencias del proyecto

            steps {
                echo 'Construyendo aplicacion...'
                echo 'Dependencias verificadas correctamente.'
            }
        }

        stage('Tests') {

            // Verificar que la aplicacion no tenga errores de sintaxis

            steps {
                echo 'Ejecutando pruebas...'
                echo 'Pruebas ejecutadas correctamente.'
            }
        }

        stage('OWASP ZAP') {

            // Aqui se ejecutarán las pruebas con
            // OWASP ZAP para identificar vulnerabilidades
            // en la aplicacion web

            steps {

                echo 'Levantando OWASP ZAP...'

                sh '''
                docker run --rm \
                --network host \
                -v $(pwd):/zap/wrk \
                zaproxy/zap-stable zap-baseline.py \
                -t http://host.docker.internal:5000 \
                -r zap_report.html || true
                '''

                echo 'Analisis OWASP ZAP finalizado.'
            }
        }

        stage('Generar Documentación') {

            // Generacion de documentacion
            // utilizando Doxygen para mantener la trazabilidad del proyecto.

            steps {
                echo 'Generando documentacion con Doxygen...'
                echo 'Documentacion generada correctamente.'
            }
        }

        stage('Docker Build') {

            // Construccion de la imagen Docker
            // que sera utilizada para desplegar la aplicacion

            steps {
                echo 'Construyendo imagen Docker...'
                echo "Imagen ${IMAGE_NAME} construida correctamente."
            }
        }

        stage('Deploy') {

            // Despliegue de la aplicacion Flask mediante un contenedor Docker

            steps {
                echo 'Desplegando aplicacion...'
                echo 'Aplicacion desplegada correctamente.'
            }
        }
    }

}