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
    }
}