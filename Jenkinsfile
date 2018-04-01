pipeline {
	agent {
		docker {
			image 'maven:3-alpine'
			args '-v /root/.m2:/root/.m2'
		}
	}

	stages {
		stage('Build') {
			steps {
				sh 'mvn -B -D skipTests clean package'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			      }
			
			post {
				always {
					junit 'target/surefire-reports/*.xml'
				}
			}
		}
		stage('Deliver') {
			steps {
				sh './jenkins/scripts/deliver.sh'
			}
		}
		stage("Docker") {
			steps {
				sh 'echo ${workspace}
				dir(${workspace}){ 
				sh 'docker build -t devblueray/maven-tutorial:v1 .'
				}

			}
		}
	}
	
}

