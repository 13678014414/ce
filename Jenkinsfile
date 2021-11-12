pipeline {
    agent any
    stages {
      stage('donet-publish') {
        steps {
            sh 'dotnet publish --configuration Release -o ${PUBLISH_PATH}'
          }
        }
      stage('docker publish') {
        steps {
          sh '(docker rm -f ${CURRENT_CONTAINER_NAME} && docker rmi -f ${CURRENT_IMAGE_NAME}:${VERSION}) || echo "continue execute"'
          sh '''cd ${PUBLISH_PATH}
                docker build -t ${CURRENT_IMAGE_NAME}:${VERSION} .'''
          }
        }
      stage('docker run') {
          steps {
            sh 'docker run --name=${CURRENT_CONTAINER_NAME} -p ${PORT}:80 --restart=always -d  ${CURRENT_IMAGE_NAME}:${VERSION}'
          }
        }
     }
    
    
    environment {
    PUBLISH_FRAMEWORK = 'cc.1'
	PUBLISH_RUNTMIE = 'centos.7.5-x64'
    PUBLISH_PATH = 'publish'
    VERSION=1.0
    ROOT_PATH = '1cc'
    PROJECT_NAME = '2cc'
    CURRENT_IMAGE_NAME = '3cc'
    CURRENT_CONTAINER_NAME = '4cc'
    PORT=80
   }
}
