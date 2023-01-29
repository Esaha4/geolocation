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
                nexusArtifactUploader artifacts: 
                [[artifactId: '${POM_ARTIFACTID}', 
                classifier: '', 
                file: 'target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}', 
                type: '${POM_PACKAGING}']], 
                credentialsId: 'NexusID', 
                groupId: '${POM_GROUPID}', 
                nexusUrl: '192.168.56.12:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'biom', 
                version: '${POM_VERSION}'
            }
        }
         stage('list containt') {
            steps {
                sh'ls'
            }
        }
       
    }
}