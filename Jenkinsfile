pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { cron('H/45 * * * 1-5') }
    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/CI-CDProjects/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('Build') {
        tools {
            jdk 'openjdk_8'
            }
            steps {
                sh 'mvn package'
            }
        }
        stage('Archive the Package') {
            steps {
                archiveArtifacts onlyIfSuccessful: true,
                    artifacts: '**/target/gameoflife.war',
                    allowEmptyArchive: false
            }
        }
        stage('Publish the Test Results') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml',
                allowEmptyResults: true
            }
        }
    }
}