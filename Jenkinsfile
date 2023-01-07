pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/dir07/maven-xml-hello-world.git'
                sh "clean package"
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.war'
                }
            }
        }
        stage ('tomcat') {
            steps {
                deploy adapters: [tomcat7(credentialsId: 'tom', path: '', url: 'http://IP:8080/')], contextPath: 'tomc', war: '**/*.war'
            }
        }
    }
}
