node {
    def app
    environment {
        DOCKER_HOST = "tcp://docker-1:2375"
    }
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        script {
            app = docker.build("marijadimitrieska/kiii-jenkins")
        }
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
        }
    }
}
