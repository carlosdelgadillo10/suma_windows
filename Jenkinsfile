node {
    def application = "suma_windows"
    def dockerhubaccountid = "carlosdelgadillo"
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "https://registry.hub.docker.com" ]) {
        app.push()
        app.push("latest")
    }
    }

    stage('Deploy') {
        sh ("docker run -d -p 8001:8001 ${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Remove old images') {
        // remove old docker images
        sh("docker rmi ${dockerhubaccountid}/${application}:latest -f")
   }
}