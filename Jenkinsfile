currentBuild.displayName = "JD-Networks-#"+currentBuild.number

pipeline{
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('build docker image'){
            steps{
                sh "docker build . -t jddivak/demo-app:${DOCKER_TAG}"
            }
         }
        stage('DockerHub Push'){
            steps{
            withCredentials([string(credentialsId: 'DockerHub', variable: 'DockerHub')]) {
                sh "docker login -u jddivak -p ${DockerHub}"
                sh "docker push jddivak/demo-app:${DOCKER_TAG}"
            }
          }
        }
     }
  }


def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
