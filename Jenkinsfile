pipeline {
    environment {
        imagename = "the-example-app:${env.BUILD_ID}"
        registryCredential = 'liorbenami-dockerhub'
        dockerImage = ''
        imageTestName = "the-example-app-test:${env.BUILD_ID}"
        dockerTestImage = ''
  }
    agent any
    stages {
        stage ('Checkout') {
          steps {
            git \
            branch: 'liorbenami_docker_br', \
            url: 'https://github.com/liorbenami1/the-example-app.nodejs.git'
          }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build imagename
                 }
                //sh 'npm install -g contentful-cli'
                //sh 'npm install'
                //sh 'npm run start:dev &'
                //sh 'mvn clean package'
                //junit '**/target/surefire-reports/TEST-*.xml'
                //archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        //stage('Building test image') {
        //    steps {
        //        script {
        //            dockerTestImage = docker.build(imageTestName, "-f Dockerfile-test .")
        //         }
        //    }
        //}
        stage('test') {
            steps {
                script {
                   dockerImage.withRun() { c ->
                       sh 'sleep 15m'
                    }
                }
                //sh 'npm run test:unit'
                //sh 'sleep 5m'
            }
        }
        stage('Deploy-to-DEV') {
            steps {
                sh 'echo Hello'
                
            }
        }
    }
}
