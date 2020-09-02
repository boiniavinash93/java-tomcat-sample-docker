pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh "mvn clean package"
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

        stage('Deploy Tomcat Docker Image'){
            steps {
                sh "docker container run -p 8088:8080 tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }

    }
}
