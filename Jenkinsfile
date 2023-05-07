node('MAVEN_JDK8') {

    stage('version control') {
        git url: 'https://github.com/wakaleo/game-of-life.git'
        branch: 'scripted'   
        }
    stage('build') {
        script: 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
        }
    stage('Archive the Artifacts') {
        archiveArtifacts onlyIfSuccessful: true,
            artifacts: '**/target/gameoflife.war',
            allowEmptyArchive: false
        }    
    stage('Publish Test Results') {
        junit testResults: '**/surefire-reports/TEST-*.xml',
              allowEmptyResults: true
        }
}