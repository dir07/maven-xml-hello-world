pipeline {
    agent any
    tools {
        maven "maven"   //maven name 9in global vtool config.
    }
    stages {
        stage('Build') {
            steps {
                //git 'https://github.com/dir07/maven-xml-hello-world.git' add git repo
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts 'target/*.war'
                }
            }
        }
        stage ('tomcat') {
            steps {
                deploy adapters: [tomcat7(credentialsId: 'tom', path: '', url: 'http://tomcatIP:8080/')], contextPath: 'tomc', war: '**/*.war'
            }
        }
    }
}
