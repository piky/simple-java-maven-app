pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /home/.m2:/usr/share/maven/ref/'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean verify'
            }
            post {
                always {
                    junit(allowEmptyResults: true,
                    testResults: 'target/surefire-reports/*.xml')
                }
            }
        }
        stage('Publish') { 
            steps {
                sh 'mvn -B -DskipTests deploy -s /usr/share/maven/ref/settings.xml'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Build ${env.JOB_NAME}: ${env.BUILD_NUMBER}"
                    echo "Current: $PWD"
                    docker.withRegistry('http://localhost:8000','docker-registry-admin') {
                        def customImage = docker.build("localhost:8000/simple-java-maven-app:${env.BUILD_NUMBER}","-f k8s/Dockerfile .")
                        customImage.push()
                    }
                }
            }
        }
    }
}