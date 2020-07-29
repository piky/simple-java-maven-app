pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /home/.m2:/root/.m2'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Verify') {
            steps {
                sh 'mvn verify'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Upload') { 
            steps {
//                sh './jenkins/scripts/deliver.sh' 
                sh 'mvn clean deploy'
            }
        }
    }
}