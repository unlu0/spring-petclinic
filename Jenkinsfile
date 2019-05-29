pipeline{
	agent{ label 'master'}
	stages{
		stage ('Checkout'){
		 steps {
		  git 'https://github.com/unlu0/spring-petclinic.git'
		 }
		}
		stage ('Build') {
		 agent{ docker 'maven:3.5-alpine'}
 		 steps {
		  sh 'mvn clean package'
		  junit '**/target/surefire-reports/TEST-*.xml'
		  archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
		 }
		}
		stage('Deploy'){
		 steps {
		   input 'Do you approve the deployment?'
		   sh 'scp target/*.jar jenkins@192.168.213.129:/opt/pet'
		   sh "ssh jenkins@192.168.213.129 'nohup java -jar /opt/pet/spring-petclinic-2.1.0.jar &'" 
		 }
		}
	}
}
