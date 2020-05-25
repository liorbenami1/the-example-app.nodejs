pipeline {
    /**
     *  In this example, the agent's Dockerfile is within the repository.
     *  Therefore, you must use this example only in "Multibranch Pipeline" or a "Pipeline from SCM".
     *  More information here: https://jenkins.io/doc/book/pipeline/syntax/#agent under "dockerfile".
     */
    agent {
        dockerfile {
            dir './'
        }
    }

    environment {
        npm_config_cache = 'npm-cache'
    }

    stages {
        stage('Artifactory configuration') {
            steps {
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
        }

        /*stage('Exec npm install') {
            steps {
                rtNpmInstall(
                        path: "./",
                        resolverId: "NPM_RESOLVER"
                )
            }
        }*/

        stage('Exec npm publish') {
            steps {
                rtNpmPublish(
                        path: "./",
                        deployerId: "NPM_DEPLOYER"
                )
            }
        }

        stage('Publish build info') {
            steps {
                rtPublishBuildInfo(
                        serverId: "ARTIFACTORY_SERVER"
                )
            }
        }
    }
}
