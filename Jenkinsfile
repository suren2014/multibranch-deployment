pipeline {
  agent { label "${LABEL_NAME}" }

  environment {
    IMAGE_NAME = netweb
    IMAGE_TAG = "${BUILD_NUMBER}"
    CONTAINER_NAME = net1
  }

  stages {
    stage('checkout') {
      steps {
        git url:"", branch:"main"
      }
    }
     stage('BUILD') {
      steps {
        sh " docker build -t $IMAGE_NAME:$IMAGE_TAG . "
      }
     }
     stage('DEPLOY') {
      steps {
        sh " docker stop $CONTAINER_NAME || true "
        sh " docker rm $CONTAINER_NAME || true "
        sh " docker run -d --name $CONTAINER_NAME -p 9000:80 restart always $IMAGE_NAME:$IMAGE_TAG "
      }
     }
  }
}
    
      
