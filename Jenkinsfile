node {
    def app
    def app-test

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("the-example-app/zerto-app")
    }

    stage('Test image') {
        app-test = docker.build("the-example-app/zerto-app", "Dockerfile-test")
        }
    }

}
