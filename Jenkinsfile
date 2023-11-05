pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = credentials('mdabudoc')
        DOCKER_HUB_PASS = credentials('dckr_pat_GLq2ckaGnmfjym7NhvjCTikgsv4')
    }
    stages {
        stage('source') {
            steps {
                git branch: 'main', url: 'https://github.com/mdabuateef/multitest.git'
            }
        }
        stage('build') {
            steps {
                script {
                    withMaven {
                        sh 'mvn clean verify sonar:sonar'
                    }
                }
            }
        }
        stage('docker-build') {
            steps {
                script {
                    sh 'sudo docker build -t docker_repo:latest /var/lib/jenkins/workspace/docker-pipe'
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    sh "docker login -u ${env.DOCKER_HUB_USER} -p ${env.DOCKER_HUB_PASS}"
                    sh "docker push mdabudoc/open:${BUILD_NUMBER}"
                }
            }
        }
    }
}

