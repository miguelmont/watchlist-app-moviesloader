def imageName = 'miguelmont/movies-loader'

node('ubuntu-2004-gce'){
    stage('Checkout'){
        checkout scm
    }

    stage('Unit Tests'){
        sh "sudo docker build -t ${imageName}-test -f Dockerfile.test ."
        sh "sudo docker run --rm -v $PWD/reports:/app/reports ${imageName}-test"
        junit "$PWD/reports/*.xml"
    }
}