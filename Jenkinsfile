pipeline {
    agent any

    stages {
        stage ('BuildStage') {

            steps {
                fileExists 'pom.xml'
                
                    sh 'mvn clean package'
               
                }
            }
        

        stage ('Upload war to nexus') {

            steps {
      
                 nexusArtifactUploader artifacts: [[artifactId: 'myweb', 
                                       classifier: '', file: 'target/myweb-1.0.0-SNAPSHOT.war', 
                                       type: 'war']], 
                                       
                     credentialsId: '534c93e0-2f0b-491c-baac-b420083e84c4', 
                     groupId: 'in.javahome', 
                     nexusUrl: '192.168.0.111:8081', 
                     nexusVersion: 'nexus3', 
                     protocol: 'http', 
                     repository: 'devops-nexus', 
                     version: '1.0.3-SNAPSHOT'
                }
            }
    }
}
