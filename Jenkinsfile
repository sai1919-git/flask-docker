pipleline{
  agent any
  environment{
      DOCKER_HUB="docker-cred-id"
      IMAGE_NAME="sai604/docker-flask"
      TAG="latest"
  }
  stages{
    stage("checkout"){
    steps{
      git https://github.com/sai1919-git/flask-docker.git
    }
    }
    stage("build image"){
    step{
      docker.build ("$IMAGE_NAME:$TAG")
    }
    }
    stage("push image"){
      steps{
        script{
        docker.withregistry('https://index.docker.io/v1',"${DOCKER_HUB}")
        docker.build("${IMAGE_NAME}:${TAG}").push()
      }
    }
    }
    stage("running"){
      steps{
         sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                docker run -d -p 5000:5000 --name flask-container ${IMAGE_NAME}:${IMAGE_TAG}
                '''
      }
    }
        
}
