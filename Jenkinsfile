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
            agent { dockerfile true}
            steps{
                sh 'chmod +x script.sh'
                sh './script.sh'
                sh 'python test_main.py'

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
        buildDiscarder logRotator(artifactDaysToKeepStr: '7', artifactNumToKeepStr: '20', daysToKeepStr: '7', numToKeepStr: '20')
        durabilityHint('SURVIVABLE_NONATOMIC ')
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