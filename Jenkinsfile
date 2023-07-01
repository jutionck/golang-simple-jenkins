pipeline {
    agent any
    stages {
        stage("Clone Source") {
            steps {
                echo 'Clone Source'
                git branch: 'main', url: 'git@github.com:jutionck/golang-simple-jenkins.git'
            }
        }

        stage("Build") {
            steps {
                echo 'Build Go'
                sh '/usr/local/go/bin/go build main.go'
            }
        }

        stage("Test") {
            steps {
                echo 'Test'
                sh 'GIN_MODE=release /usr/local/go/bin/go test -v'
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
