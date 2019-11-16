node('') {
	stage('Poll') {
		checkout scm
	}
	stage('Build & Unit test'){
		withMaven(maven:'maven'){
			bat 'mvn clean verify -DskipITs=true';}
		junit '**/target/surefire-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
	stage('Static Code Analysis'){
		withMaven(maven:'maven'){
			bat 'mvn clean verify sonar:sonar -Dsonar.projectName=exemple-sonar -Dsonar.projectKey=exemple-sonar -Dsonar.projectVersion=$BUILD_NUMBER';
		}
	}
	
	stage ('Integration Test'){
		withMaven(maven:'maven'){
			bat 'mvn clean verify -Dsurefire.skip=true';}
		junit '**/target/failsafe-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
	stage ('Publish'){
		withMaven(maven:'maven'){
			bat 'mvn deploy';}
		
	}
}
