def imageName = 'miguelmont/movies-loader'

pipeline {
    agent {
        label 'ubuntu-2004-gce'
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
        stage('Confirm'){
            steps {
                timeout(time:3, unit:"DAYS") {
                input(message: "Deploy to Stage", ok: "Yes, let's do it!")
            }
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