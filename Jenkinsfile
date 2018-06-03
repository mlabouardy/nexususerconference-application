imageName = 'nexus-user-conference/application'
registry = 'https://registry.slowcoder.com'

node('slaves'){
    stage('Checkout'){
        checkout scm
    }

    stage('Test'){
        docker.build("${imageName}:${env.BUILD_ID}", '-f Dockerfile.test .')
        sh "docker run --rm ${imageName}:${env.BUILD_ID}"
    }

    stage('Build'){
        docker.build("${imageName}")
    }

    stage('Push'){
        docker.withRegistry(registry, 'registry') {
            docker.image(imageName).push("${commitID()}")

            if (env.BRANCH_NAME == 'master') {
              docker.image(imageName).push('latest')
            }
        }
    }

    /*
    stage('Deploy'){
        build job: "nexususerconference-deployment/master"
    }*/
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}