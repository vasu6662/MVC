@Library('shared-library')
node(label: 'master')
{
//Variables
	def CONTAINER_NAME="jenkins-pipeline"
	def CONTAINER_TAG="latest"
	def gitURL = "https://github.com/vasu6662/MVC.git"
	def repoBranch = "master"
	def mvnHome = "maven"
	def sonarqubeGoal = "clean verify sonar:sonar"
	def pom = "pom.xml"
	def sonarqubeServer = "Sonarcloud"
	def goal = "clean install"

	
		//Git Stage
    stage('Git-Checkout'){
        gitClone "${gitURL}","${repoBranch}"    
    }
    
		//Sonarqube Analysis
    stage('Sonarqube-scan'){
        sonarqubeScan "${mvnHome}","${sonarqubeGoal}","${pom}", "${sonarqubeServer}"
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
	//end
