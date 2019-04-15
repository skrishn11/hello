node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "gs-springboot"
    registryHost = "127.0.0.1:3100/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName

    stage "Build/Push"

        sh "pack build shkrishnamoorthy/pksimages:gs-springboot --publish"
    
    stage "Push"

        sh "echo pack build-push complete"

    stage "Deploy"
          sh "kubectl apply -f k8s/deployment.yaml"

}