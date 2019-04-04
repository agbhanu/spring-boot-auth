pipeline{
 agent{
   docker{
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