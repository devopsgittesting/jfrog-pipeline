pipeline {
    agent any

   stages {
	    stage('Git CheckOut') {
		    steps {
			   git branch: 'main', credentialsId: 'My private token login creds', url: 'https://github.com/devopsgittesting/jfrog-pipeline.git'
			}
		}
        stage('Clean and Install') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ('Package'){
            steps {
               sh 'mvn package'
             }
        }
	stage ('Server'){
            steps {
               rtServer (
                 id: "Artifactory",
                 url: 'http://192.168.0.115:8082/artifactory',
                 username: 'admin',
                  password: 'Admin@1234',
                  bypassProxy: true,
                   timeout: 300
                        )
            }
        }

        stage('Upload'){
            steps{
                rtUpload (
                 serverId:"Artifactory" ,
                  spec: '''{
                   "files": [
                      {
                      "pattern": "*.war",
                      "target": "maven-demo-repo-libs-snapshot-local"
                      }
                            ]
                           }''',
                        )
            }
        }
	   
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Artifactory"
                )
            }
        }
    }
}
