node {
	def app
	properties([disableConcurrentBuilds()])
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build('dheerajk27/example-app')
	}

	stage('Test build'){
		app.inside{
			sh 'npm test'
		}
	}

	stage('Push image') {
		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
			app.push("${env.BRANCH_NAME}-latest")
			app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
		}
	}
}
