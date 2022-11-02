def imageName = 'miguelmont/movies-loader'

node('ubuntu-2004-gce'){
    stage('Checkout'){
        checkout scm
    }

    stage('Unit Tests'){
        sh "docker build -t ${imageName}-test -f Dockerfil.test ."
        sh "docker run --rm ${imageName}-test"
    }
}∏