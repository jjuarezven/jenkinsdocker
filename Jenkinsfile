pipeline {
	agent any
	environment {
		IMAGE = "my-image"
		DOCKER_REGISTRY = "josejuarez78"
        DOCKER_HUB_LOGIN = credentials('docker-hub')
	}
	stages {
		stage('checkout github') {
			steps {
				echo 'Descargando codigo de SCM'
				sh 'rm -rf *'
				checkout scm
			}
		}
		/* stage('check tools') {
			steps {
				sh "mvn -version"
			}
		} */
		stage('Build Node') {
			steps {
				echo 'Build Node'
				sh 'npm install'
			}
		}
	
		stage('Build docker') {
			steps {
				echo("Hago un build de docker imagen ${IMAGE}")
				sh("docker build -t ${IMAGE} .")
				sh("docker tag ${IMAGE} ${DOCKER_REGISTRY}/${IMAGE}")
			}
		}

        stage('docker deploy') {
			steps {
                echo("Hago Docker Login")
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
				sh("docker push ${DOCKER_REGISTRY}/${IMAGE}")
				/* echo("Borro la imagen ${IMAGE}:v${BUILD_RELEASE_VERSION}")
				sh("docker rmi ${IMAGE}:v${BUILD_RELEASE_VERSION}") */
			}
		} 
	}
}