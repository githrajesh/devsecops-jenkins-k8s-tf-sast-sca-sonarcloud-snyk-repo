pipeline {
    agent any
    tools {
        maven 'maven-3.9.6'
    }
    stages {
        stage ( "Checkout the Project") {
            steps {
		git branch: 'main', url:  'https://github.com/Shikhar82/devsecops-jenkins-k8s-tf-sast-sca-sonarcloud-snyk-repo.git'
            }
        }
		stage ( "Compile and Run Sonar Analysis" ) {
		steps {
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=devsecopsshikhar -Dsonar.organization=devsecopsshikhar -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=0846fc4fb99e714cef3ead084f4c46424e1eb8a0'
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
