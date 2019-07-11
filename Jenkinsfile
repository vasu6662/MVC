@Library('shared-library') _
node(label: 'master'){

 def CONTAINER_NAME="jenkins-pipeline"
	def CONTAINER_TAG="latest"
	def gitURL = "https://github.com/vasu6662/MVC.git"
	def repoBranch = "master"
	def mvnHome = "maven"
	def sonarqubeGoal = "clean verify sonar:sonar"
	def pom = "pom.xml"
	def sonarqubeServer = "sonar"
	def goal = "clean install"

	
		//Git Stage
    stage('Git-Checkout'){
        gitClone "${gitURL}","${repoBranch}"    
    }
    
		//Sonarqube Analysis
    stage('Sonarqube-scan'){
      //  sonarqubeScan "${mvnHome}","${sonarqubeGoal}","${pom}", "${sonarqubeServer}"
      sh "mvn sonar:sonar \
  -Dsonar.projectKey=Devops_test \
  -Dsonar.organization=vasuabc \
  -Dsonar.host.url=https://sonarcloud.io \
  -Dsonar.login=8fbc5c9b24e07c8b4473c2ccdb6793e975ad261a"
    }
    
    
		//Quality-gate
    stage('Quality-Gate'){
        qualityGate "${sonarqubeServer}"
    }

		//MVN Build
    stage('Maven Build'){
        mavenBuild "${mvnHome}","${pom}", "${goal}"
	}
}
