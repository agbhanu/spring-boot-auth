pipeline{
 agent{
   docker{
     args '-v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock'
     image 'gradle:jdk8-slim'
   }
 }
 stages{
    stage("clean project"){
      steps{
        sh "./gradlew clean"
      }
    }
    stage("build docker image"){
      steps{
        echo 'Starting to build docker image'

          script {
            def customImage = docker.build("my-image:${env.BUILD_ID}")
            customImage.push()
          }
      }
    }
 }
}