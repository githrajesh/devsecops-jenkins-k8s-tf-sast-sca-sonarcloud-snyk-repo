pipeline {
    agent any
    tools {
        maven 'maven-3.9.6'
    }
    stages {
        stage ( "Checkout the Project") {
            steps {
		git branch: 'main', url:  'https://github.com/githrajesh/devsecops-jenkins-k8s-tf-sast-sca-sonarcloud-snyk-repo.git'
            }
        }
		stage ( "Compile and Run Sonar Analysis" ) {
		steps {
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=DevSecOpsLearn -Dsonar.organization=DevSecOpsLearn -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=SONAR_TOKEN2'
		}
		}
	    	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
		}
    }
}
