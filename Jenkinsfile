pipeline {
    agent any
    stages {
        stage('UnitTest') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Publish') { 
            steps {
                sh 'mvn deploy'
            }
        }
    }
}