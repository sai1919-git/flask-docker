pipeline{
  agent any
  environment{
      DOCKER_HUB="docker-cred-id"
      IMAGE_NAME="sai604/flask-docker"
      TAG="latest"
  }
  stages{
    stage("checkout"){
    steps{
     git url: 'https://github.com/sai1919-git/flask-docker.git', branch: 'main'

    }
    }
    stage("build image"){
    steps {
      script{
      dockerImage=docker.build ("$IMAGE_NAME:$TAG")
    }
    }
    }
    stage("push image"){
      steps{
        script{
        docker.withRegistry('https://index.docker.io/v1',"${DOCKER_HUB}") {
        dockerImage.push()
      }
        }
    }
    }
    stage("running"){
      steps{
         sh '''
                docker stop flask-container || true
                docker rm flask-container || true
                docker run -d -p 5000:5000 --name flask-container ${IMAGE_NAME}:${TAG}
                '''
      }
    }
  }
        
}
