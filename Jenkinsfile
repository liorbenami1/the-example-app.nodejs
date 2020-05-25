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

    stage('Deploy image') {
	sh 'echo "deploy"'	
    }
}
