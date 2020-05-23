	node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        /*app = docker.build("getintodevops/hellonode")*/
        app = docker.build("the-example-app/zerto-app")
    }

    stage('Run image') {

        /*app = docker.build("getintodevops/hellonode")
        app = docker.run("the-example-app/zerto-app")*/
        sh 'docker container run --detach --publish 3000:3000 --name app_zerto the-example-app/zerto-app'
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
           /* sh 'npm run test'*/
           sh 'echo "test success"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. 
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') { 
        docker.withRegistry('https://hub.docker.com/repository/docker/liorbenami/linux_tweet_app', 'docker-hub-credentials') { */
        docker.withRegistry('https://registry.hub.docker.com', '0cc1dad5-db19-4d25-a236-df4286458fc7') { 
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
