pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                // Updated to use Maven 3.9.9 and JDK 21 to pass the Enforcer check
                bat 'docker run --rm -v "%WORKSPACE%":/usr/src/mymaven -w /usr/src/mymaven maven:3.9.9-eclipse-temurin-21-alpine mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'docker run --rm -v "%WORKSPACE%":/usr/src/mymaven -w /usr/src/mymaven maven:3.9.9-eclipse-temurin-21-alpine mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                bat 'jenkins\\scripts\\deliver.bat'
            }
        }
    }
}
