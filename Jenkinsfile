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
                    [[artifactId: "${mavenPom.artifactId}", 
                    classifier: '', 
                    file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}", 
                    type: "${mavenPom.packaging}"]], 
                    credentialsId: 'NexusID', 
                    groupId: "${mavenPom.groupId}", 
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