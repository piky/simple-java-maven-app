pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
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
                nexusPublisher nexusInstanceId: 'dev-repo', nexusRepositoryId: 'simple-java-maven-app', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'simple-java-maven-app', groupId: 'th.co.aspiron.app', packaging: 'jar', version: '1.0.0-SNAPSHOT']]]
            }
        }
    }
}