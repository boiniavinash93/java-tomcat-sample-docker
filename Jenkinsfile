pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                def mvnHome = tool name: 'Apache Maven 3.6.3', type: 'maven'
                sh "${mvnHome}/bin/mvn -f pom.xml clean package"
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }

    }
}