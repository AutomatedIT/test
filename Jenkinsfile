#!groovy

def app = 'nginx'
def stages = env.STAGE ?: 'build,start,test,tear'
def version = env.VERSION ?: "0.0.{BUILD_ID}".toString()

node() {

  deleteDir()
  stage('checkout') {
    git(
        url: 'https://github.com/test1",
        branch: master
        )
   }

  stage('Build Images') {
    sh """
      sudo docker build -t ${app} ${app}/
      sudo docker images | grep ${app}
      """
  }

  stage('Start Container') {
    sh """
       sudo docker run -d -p 8082:80 --name ${app}-dev ${app}
       curl -s localhost:8082
       """
  } 

  stage('Teardown') {
     sh """
        sudo docker stop ${app}-dev 
        sudo docker rm ${app}-dev 
        """

  }

}
