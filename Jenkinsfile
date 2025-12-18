pipeline
	agent any
	
	stages{
		stage('scm'){
			steps{
				checkout scm
			}
		}
		stage('build'){
			steps{
				sh 'mvn clean install'
			}
		
		}
		stage('nexus'){
			steps{
				nexusArtifactUploader artifacts: [
				[
				artifactId: 'onlinebookstore', 
				classifier: '', 
				file: '/var/lib/jenkins/workspace/onlinebookstores/target/onlinebookstore-0.0.1-SNAPSHOT.war', 
				type: 'war'
				]
				], 
				credentialsId: 'nexus', 
				groupId: 'onlinebookstore', 
				nexusUrl: '34.224.102.42:8081', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'onlinebookstores', 
				version: '0.0.1-SNAPSHOT'
			}
		}
		stage('deploy'){
			steps{
				deploy adapters: [
				tomcat9
				(
				alternativeDeploymentContext: '', 
				credentialsId: 'tomcat', 
				path: '', 
				url: 'http://23.21.15.191:8090/')], 
				contextPath: null, 
				war: '**/*.war'
			}
		}
	}
