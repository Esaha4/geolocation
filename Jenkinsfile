pipeline {

    agent Built-In Node
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
       
    }
}