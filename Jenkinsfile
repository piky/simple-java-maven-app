pipeline {
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Publish') { 
            steps {
                sh 'mvn deploy'
//                nexusPublisher nexusInstanceId: 'dev-repo', nexusRepositoryId: 'simple-java-maven-app', packages: []
            }
        }
    }
}