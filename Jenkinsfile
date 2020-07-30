pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /var/jenkins_home/.m2:/root/.m2'
        }
    }
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