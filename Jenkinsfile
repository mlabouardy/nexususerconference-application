imageName = "nexususerconference-application"

node('slaves'){
    stage('Checkout'){
        checkout scm
    }

    stage('Test'){
        docker.build("${imageName}:${env.BUILD_ID}", "-f Dockerfile.test .")
        sh "docker run --rm ${imageName}:${env.BUILD_ID}"
    }

    stage('Build'){
        docker.build("${imageName}")
    }

    stage('Push'){

    }

    stage('Deploy'){

    }
}