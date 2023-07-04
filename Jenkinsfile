pipeline {
    agent any
    environment {
        GIT_URL = 'git@github.com:jutionck/golang-simple-jenkins.git'
        BRANCH = 'with-docker'
        CHANNEL = '#training'
        IMAGE = 'my-golang-test'
        CONTAINER = 'my-golang-test-app'
        DOCKER_APP = '/usr/local/bin/docker'
    }
    stages {
        stage("Cleaning up") {
            steps {
                echo 'Cleaning up'
                sh "${DOCKER_APP} rm -f ${CONTAINER} || true"
            }
        }

        stage("Clone") {
            steps {
                echo 'Clone'
                git branch: "${BRANCH}", url: "${GIT_URL}"
            }
        }

        stage("Build and Run") {
            steps {
                echo 'Build and Run'
                sh "DB_HOST=product-db DB_PORT=5433 DB_NAME=postgres DB_USER=postgres DB_PASSWORD=P@ssw0rd API_PORT=8080 ${DOCKER_APP} compose up"
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            slackSend(channel: '#training', message: "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}
