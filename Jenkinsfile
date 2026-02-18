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
        git url:"https://github.com/suren2014/multibranch-deployment.git", branch:"main"
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
        sh " docker run -d --name $CONTAINER_NAME -p 9001:80 restart always $IMAGE_NAME:$IMAGE_TAG "
      }
     }
  }
  post {
    success {
      clean Ws()
    }
    failure {
      echo "PIPELINE FAILED, PLEASE CHECK THE LOGS"
    }
  }
}
    
      
