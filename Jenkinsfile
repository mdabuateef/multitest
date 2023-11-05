pipeline {
	agent any 
	
	environment {
		DOCKER_HUB_USER = credentials('mdabudoc') 
                DOCKER_HUB_PASS = credentials('dckr_pat_GLq2ckaGnmfjym7NhvjCTikgsv4')
	stages { 
		stage('source') {
			steps {
				git branch: 'main', url: ''https://github.com/mdabuateef/multitest.git'
				}
			}
		stage('build') {
			step {
				withMaven {
					sh 'mvn clean verify sonar:sonar'
					}
				}
			}
		stage('docker-build') {
			step {
				sh 'sudo docker build -t dock /var/lib/jenkins/workspace/docker-pipe/Dockerfile'
				}
			}
		stage('deploy') {
			step {
				sh "docker login -u ${env.DOCKER_HUB_USER} -p ${env.DOCKER_HUB_PASS}"
				sh "docker image push docker:${BUILD_NUMBER}"
				}
			}
		}
	}
}
