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
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                nexusPublisher nexusInstanceId: 'dev-repo', nexusRepositoryId: 'simple-java-maven-app', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'my-app', groupId: 'om.mycompany.app', packaging: 'jar', version: '1.0-SNAPSHOT']]]
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}