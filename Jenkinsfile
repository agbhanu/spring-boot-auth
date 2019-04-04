pipeline{
 agent{
   docker{
     image 'gradle:jdk8-slim'
   }
 }
 stages{
    stage("build docker image"){
      steps{
        docker.build("spring-boot-image")
      }
    }
 }
}