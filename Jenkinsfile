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

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused.*/
        docker.withRegistry('http://15.185.96.125/artifactory', 'artifactory-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
