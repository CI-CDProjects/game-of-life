pipeline {
    agent { label 'MAVEN_JDK8' }
    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/CI-CDProjects/game-of-life.git'
                    branch: 'declarative'
            }
        }
        stage('Build') {
            steps {
                script: 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH"' && 'mvn package'
            }
        }
        stage('Archive the Package') {
            steps {
                archiveArtifacts onlyIfSuccessful: true
                    artifacts: '**/target/gameoflife.war'
                    allowEmptyArchive: false
            }
        }
        stage('Publish the Test Results') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                allowEmptyResults: true
            }
        }
    }
}