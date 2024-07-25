pipeline {
    agent any

    tools {
        maven 'demo-app'
    }

    stages {
        stage('SCM') {
            steps {
                // Se coloca el checkout dentro de un bloque steps
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('ConJenkins') { // Asegúrate de que 'ConJenkins' sea el nombre correcto de tu configuración de SonarQube en Jenkins
                    // Ejecutar Maven directamente sin asignar a una variable
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=con-jenkins -Dsonar.projectName='con-jenkins'"
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