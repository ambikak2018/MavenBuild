node('master') {

	def MVNHOME = tool 'Maven'
	
stage ('checkout code'){
	checkout scm
}
	
stage ('build'){
	bat "${MVNHOME}/bin/mvn clean install"
}

stage ('Test Cases Execution'){
	bat "${MVNHOME}/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
}
	
stage ('Integration Test'){
	bat ""
}

stage ('Sonar Analysis'){
	//sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000/sonar'
}
	
stage('Code Coverage ') {
    //sh "curl -o coverage.json 'http://35.154.151.174:9000/sonar/api/measures/component?componentKey=com.java.example:java-example&metricKeys=coverage';sonarCoverage=`jq '.component.measures[].value' coverage.json`;if [ 1 -eq '\$(echo '\${sonarCoverage} >= 50'| bc)' ]; then echo 'Failed' ;exit 1;else echo 'Passed'; fi"
   }

stage ('Archive Artifacts'){
	archiveArtifacts artifacts: 'target/*.war'
}

//input message: "QA Team Approval for Production Deployment?"

stage ('Production Deployment'){
	bat 'copy target\\*.war C:\\Apache\\tomcat\\webapps'
}
}
