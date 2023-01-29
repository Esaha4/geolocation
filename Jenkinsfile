pipeline {

    agent any
    tools {
        maven 'M2_HOME'
    }
  
    stages {
        stage('maven package') {
            steps {
                sh'mvn clean'
                sh'mvn install'
                sh'mvn package'
            }
        }
         stage('upload artifact') {
            steps {
                script{                
                def mavenPom = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: 
                [[artifactId: "${mavenPom.artifactid}", 
                classifier: '', 
                file: "target/${mavenPom.artifactid}-${mavenPom.version}.${mavenPom.packaging}", 
                type: "${mavenPom.packaging}"]], 
                credentialsId: 'NexusID', 
                groupId: "${mavenPom.groupid}", 
                nexusUrl: '192.168.56.12:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'biom', 
                version: "${mavenPom.version}"
                }
                }
        }
         stage('list containt') {
            steps {
                sh'ls'
            }
        }
       
    }
}