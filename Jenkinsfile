def imageName = 'miguelmont/movies-loader'

pipeline {
    agent {
        docker 'jenkins/ssh-agent:alpine'
    }
    stages {
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        stage('Unit Tests'){
            steps{
                sh "sudo docker build -t ${imageName}-test -f Dockerfile.test ."
                sh "sudo docker run --rm ${imageName}-test"

            }
        }
    }
    post{
        success {
            slackSend(color:'GREEN', message: "${env.JOB_NAME} Successful build")
        }
        failure{
            slackSend(color: 'RED',  message: "${env.JOB_NAME} Failed build")
        }
    }
}