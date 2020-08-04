pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean verify'
            }
        }
        stage('Publish') { 
            steps {
                sh 'mvn deploy'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Build ${env.JOB_NAME}: ${env.BUILD_NUMBER}"
                    echo "Current: $PWD"
                    docker.withRegistry('http://localhost:8001','docker-registry-admin') {
                        def customImage = docker.build("localhost:8001/simple-java-maven-app:${env.BUILD_NUMBER}","-f k8s/Dockerfile .")
                        customImage.push()
                    }
                }
            }
        }
    }
}