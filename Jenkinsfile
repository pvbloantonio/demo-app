pipeline {
    agent any

    tools {
        maven 'Default Maven' // Asegúrate de que 'Default Maven' está configurado en Jenkins
    }

    stages {
        stage('SCM') {
            steps {
                // El checkout debe estar dentro de un bloque steps
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Ejecutar Maven y SonarQube dentro de un entorno SonarQube configurado, todo en bloques steps
                withSonarQubeEnv('ConJenkins') { // Asegúrate de que 'ConJenkins' es el nombre correcto de tu entorno SonarQube en Jenkins
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=ConJenkins -Dsonar.projectName='ConJenkins'"
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Aquí puedes agregar tus comandos de compilación, por ejemplo:
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Aquí puedes agregar tus comandos de prueba, por ejemplo:
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Aquí puedes agregar tus comandos de despliegue, por ejemplo:
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}