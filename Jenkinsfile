pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { pollSCM('* * * * *') }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'This is a Maven goal.')
    }
    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/CI-CDProjects/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('Build the Package') {
        tools {
            jdk 'openjdk_8'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
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