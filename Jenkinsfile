node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'rajuvarma12345/jfirstrepo'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/rmaheshvarma/dockertest.git'
	}
	stage('Build') {
		sh 'npm install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://registry.hub.docker.com/repository/docker/rajuvarma12345/jfirstrepo', registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://registry.hub.docker.com/repository/docker/rajuvarma12345/jfirstrepo', registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
