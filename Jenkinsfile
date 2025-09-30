pipeline {
    agent any
   environment {        
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\resources\\bin'
        PATH = "${DOCKER_PATH};${env.PATH}"
    }
    tools {
        maven 'Maven3'    // Nombre EXACTO configurado en Jenkins -> Global Tool Configuration
        jdk 'Java21'      // O el que hayas configurado (ej: Java17)
    }

    stages {
        stage('Checkout') {
     steps {
                git branch: 'master', url: 'https://github.com/vllumiquinga/eureka.git', credentialsId: 'github-credentials'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t eureka .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker stop eureka || true && docker rm eureka || true'
                sh 'docker run -d -p 8081:8081 --name eureka eureka'
            }
        }
    }
}