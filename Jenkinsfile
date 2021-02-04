pipeline {
    agent any
    stages {
        stage ('Checkout') {
          steps {
            git \
            branch: 'liorbenami_docker_br', \
            url: 'https://github.com/liorbenami1/the-example-app.nodejs.git'
          }
        }
        stage('Build') {
            steps {
                sh 'docker build . -t the-example-app:${env.BUILD_ID}")'
                //sh 'npm install -g contentful-cli'
                //sh 'npm install'
                //sh 'npm run start:dev &'
                //sh 'mvn clean package'
                //junit '**/target/surefire-reports/TEST-*.xml'
                //archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('unit-test') {
            steps {
                sh 'echo Hello'
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
