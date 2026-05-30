pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                // We use a clean Docker container command directly to bypass the Windows path bug
                bat 'docker run --rm -v "%WORKSPACE%":/usr/src/mymaven -w /usr/src/mymaven maven:3.9.6-eclipse-temurin-17-alpine mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'docker run --rm -v "%WORKSPACE%":/usr/src/mymaven -w /usr/src/mymaven maven:3.9.6-eclipse-temurin-17-alpine mvn test'
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
