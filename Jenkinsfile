pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                // Se coloca el checkout dentro de un bloque steps
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Se define y utiliza Maven dentro del bloque steps. Además, es necesario especificar el entorno de SonarQube.
                def mvn = tool 'Default Maven';
                withSonarQubeEnv('ConJenkins') { // Asegúrate de reemplazar 'My SonarQube Server' con el nombre de tu configuración de SonarQube en Jenkins
                    sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=con-jenkins -Dsonar.projectName='con-jenkins'"
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Aquí puedes agregar tus comandos de compilación, por ejemplo:
                // sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Aquí puedes agregar tus comandos de prueba, por ejemplo:
                // sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Aquí puedes agregar tus comandos de despliegue, por ejemplo:
                // sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}