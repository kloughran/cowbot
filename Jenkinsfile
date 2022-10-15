pipeline {
    agent any 
	
	stages {
		stage('remove old') { 
			steps {
				sh 'docker stop cowbot || true'
				sh 'docker rm cowbot || true'
			}
		}
		stage('update') {
			steps {
				withCredentials([usernamePassword(credentialsId: 'dockercreds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
				  sh 'docker login --username $USERNAME --password $PASSWORD'
				}
				sh 'docker pull kloughran47/home:cowbot'
			}
		}
		stage('deploy') {
			steps {
				sh 'docker run -d --name cowbot --privileged --restart unless-stopped kloughran47/home:cowbot'
			}
		}
	}
}