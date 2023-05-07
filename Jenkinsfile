node('MAVEN_JDK8') {
    
    stage('version control') {
        git url: 'https://github.com/wakaleo/game-of-life.git'
        branch: 'scripted'   
        }
    stage('build') {
        script: 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
        }
    stage('postbuild') {
        archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false
        junit '**/surefire-reports/TEST-*.xml'
        }
}