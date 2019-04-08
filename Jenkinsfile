def customImage
pipeline{
 agent{
   docker{
     args '-v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock'
     image 'gradle:jdk8-slim'
   }
 }
 stages{

    stage("install libltdl7"){
      steps{
        sh "apt-get update"
        sh "apt-get install -y libltdl7"
      }
    }
    stage("clean project"){
      steps{
        sh "./gradlew clean"
      }
    }
    stage("Build project"){
      steps{
        sh "./gradlew build"
      }
    }
    //stage("build docker image"){
      //steps{
        //echo 'Starting to build docker image'

          //script {

          //}
      //}
    //}
    stage("build and push docker image"){
      steps{
          script{
            docker.withRegistry('https://git.persistent.co.in' , 'gitlab_cred'){
              customImage = docker.build("git.persistent.co.in:4567/testgroup/springboot-docker-sample")
              customImage.push("latest")
            }
          }
      }
    }
 }
}