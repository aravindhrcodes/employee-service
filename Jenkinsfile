pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/AryanKulathinal/project1-employee-service.git', branch: 'main'
            }
        }
        stage('Pre_Build'){
            steps {
                bat "docker rm -f employee_container"
                bat "docker rmi -f employee_image"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {

                bat "docker build -t employee_image ."
                bat "docker run -p 8082:8082 -d --name employee_container employee_image"
            }
        }
    }
}
