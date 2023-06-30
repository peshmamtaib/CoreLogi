pipeline{
    agent any
    tools{
        maven "Maven-3.8.7"
    }
    stages{
        stage("Git Checkout"){
            steps{
            checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: 'aa2d34e3-60d1-47f6-8d13-69826339c502', url: 'https://github.com/peshmamtaib/CoreLogi.git']])
            }
        }
        stage("Build Artifact"){
            steps{
                sh "mvn package -f pom.xml"
            }
        }
        stage("Tomcat Deploy"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '3b6f649b-9af4-4965-9d03-2b1faaed1fd6', path: '', url: 'http://34.125.206.16:8090/')], contextPath: null, war: '**/*war'
            }
        }
        stage("Nexus Upload"){
            steps{
             nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/Test-PollSCM-Corelogic-Latest.war', type: 'war']], credentialsId: '4cfd4bf3-2347-414d-9ab3-48d43921200c', groupId: 'com.adaequare', nexusUrl: '34.125.17.131:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
    }
    
}
