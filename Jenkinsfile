node('slave1'){
    def mavenHome = tool name: 'maven', type: 'maven'
    sh "${mavenHome}/bin/mvn -v"

    stage('GitPull')
    {
          echo 'git pull '
          git 'https://github.com/penvid/webappformac.git'

    }
    stage('Build')
    {
        echo 'Build stage'
        sh "${mavenHome}/bin/mvn package -f $WORKSPACE/pom.xml"
    }
    stage('Junit testing')
    {
        echo 'mvn test'
    }
    stage('upload to nexus')
    {
        echo 'nexus'
        nexusArtifactUploader artifacts: [[artifactId: 'webappformac', classifier: '', file: '/home/jenkins/jenkins_slave/workspace/webappformac/target/webappformac.war', type: 'war']], credentialsId: 'nexus-cred', groupId: 'com.mywebproject', nexusUrl: '127.0.0.1:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.1-SNAPSHOT'
    }
    stage('Deploy')
    {
        echo 'deployed'

    }

}
