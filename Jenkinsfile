pipeline {
    agent any
    stages {
		stage('Checkout'){
		steps {
		checkout([$class: 'GitSCM', branches: [[name: '*/master']],
		doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [],
		userRemoteConfigs: [[credentialsId: '3f468ed0-fea8-4ab3-80ac-bff73343900a',
		url: 'https://github.com/arvindpathare/docker-version.git']]])}
		}
        stage('Build') {
            steps {
                script {
                    def version = readFile('VERSION')
                    def versions = version.split('\\.')
                    def major = versions[0]
                    def minor = versions[0] + '.' + versions[1]
                    def patch = version.trim()
                    docker.withRegistry('', 'my-dockerhub-credentials') {
                        def image = docker.build('arvindpathare/maven:latest')
                        image.push()
                        image.push(major)
                        image.push(minor)
                        image.push(patch)
                    }
                }
            }
        }
    }
}