pipeline {
    agent any

    tools {
        maven 'iti'
        jdk 'jdk-17'
    }

    environment {
        SERVER_PORT = '9090'
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }

        stage('Check Versions') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Run Application') {
            steps {

                sh 'nohup java -jar target/*.jar --server.port=${SERVER_PORT} > app.log 2>&1 &'

                sh 'sleep 300'
            }
        }
    }
}
