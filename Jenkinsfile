pipeline {
	agent any
	environment {
		IMAGE = "jenkins-cicd-sample"
		DOCKER_REGISTRY = "josejuarez78"
        DOCKER_HUB_LOGIN = credentials('docker-hub')
	}
	stages {
		stage('checkout github') {
			steps {
				echo 'Downloading source code from repository'
				sh 'rm -rf *'
				checkout scm
			}
		}
		stage('Build Node') {
			steps {
				echo 'Build Node'
				sh 'npm install'
			}
		}	
		stage('Build docker') {
			steps {
				echo("Building docker image ${IMAGE}")
				sh("docker build -t ${IMAGE} .")
				sh("docker tag ${IMAGE} ${DOCKER_REGISTRY}/${IMAGE}")
			}
		}
        stage('docker deploy') {
			steps {
                echo("Deploying image to docker hub")
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
				sh("docker push ${DOCKER_REGISTRY}/${IMAGE}")
			}
		} 
	}
}
