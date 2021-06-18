pipeline{
    agent any
    tools {
        maven 'maven'
        }
    environment {
      DOCKER_TAG = getVersion()
        }


    stages{
        stage('SCM'){
             steps{
            git 'https://github.com/srikanthweb/my-app-code.git'
             }
        }
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage('Docker Build'){
            steps{
            sh "docker build . -t sri2323/udemy-app:${DOCKER_TAG}"
            }
        }
       stage('DockerHUb Push'){
            steps{
                withCredentials([string(credentialsId: 'DockerHub_jun18', variable: 'dockerHubPwd')]) {
                    sh "docker login -u sri2323 -p ${dockerHubPwd}"
            }
                
            sh "docker push sri2323/udemy-app:${DOCKER_TAG}"
            }
        }
       
    }
}
def getVersion(){
  def commitHash= sh returnStdout: true, script: 'git rev-parse --short HEAD'
  return commitHash
    
}
