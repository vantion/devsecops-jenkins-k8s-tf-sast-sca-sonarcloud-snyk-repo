pipeline {
  agent any
  tools { 
        maven 'Maven_3.5.2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=sonarcloudwebapp -Dsonar.organization=sonarcloudwebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=7150f650764348acd8a5c1d6ff19b6c50ae2dc7a'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'e650f9b6-185b-49ba-86b7-c9a5b7901197', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
