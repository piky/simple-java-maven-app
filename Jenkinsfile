pipeline {
    agent any
/*     agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    } */
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('UnitTest') {
            steps {
                sh 'mvn clean test'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn verify'
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