def imageName = 'mlabouardy/movies-loader'
def registry = 'https://registry.slowcoder.com'

node('workers'){
    stage('Checkout'){
        checkout scm
    }

    stage('Unit Tests'){
         sh "docker build -t ${imageName}-test -f Dockerfile.test ."
         sh "docker run --rm -v $PWD/reports:/app/reports ${imageName}-test"
         junit "$PWD/reports/*.xml"
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}