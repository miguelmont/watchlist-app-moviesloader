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
        stage("Fix the permission issue") {
            steps {
                sh "sudo chown root:jenkins /run/docker.sock"
            }
        }
        stage('Unit Tests'){
            steps{
                sh "docker build -t ${imageName}-test -f Dockerfile.test ."
                sh "docker run --rm ${imageName}-test"

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
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '7', numToKeepStr: '20')
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