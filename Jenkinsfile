node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("the-example-app/zerto-app:${env.BUILD_ID}")
    }

    stage('Test image') {
        docker.build("the-example-app/zerto-app:${env.BUILD_ID}", "-f Dockerfile-test .")
    }

    stage('Artifactory configuration') {
	rtServer(
        	id: "zerto-artifactory",
		url: "http://15.185.96.125:8081/artifactory",
		credentialsId: "artifactory-credentials"
	)
	rtNpmResolver(
		id: "NPM_RESOLVER",
		serverId: "zerto-artifactory",
		repo: "npm-remote"
	)
	rtNpmDeployer(
		id: "NPM_DEPLOYER",
		serverId: "zerto-artifactory",
		repo: "npm-local"
	)
    }
    
    /*(stage('Exec npm install') {
	rtNpmInstall(
		path: "",
		resolverId: "NPM_RESOLVER"
	)
    }*/

    stage('check if manual') {
	if(currentBuild.rawBuild.getCause()[0].toString().contains('UserIdCause')){
		sh 'echo "this is a manual trigger, going to deploy to Staging environment..."'
	}
    }
}
