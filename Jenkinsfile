pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17-alpine'
           
            args '-v /var/run/docker.sock:/var/run/docker.sock'
            customWorkspace '/data/jenkins_home/workspace/MyPipeline_main'
        }
    }
    stages {
        stage('Build') {
            steps {
               
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
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
