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
        sh "./gradle build"
      }
    }
    //stage("build docker image"){
      //steps{
        //echo 'Starting to build docker image'

          //script {

          //}
      //}
    //}
    //stage("build and push docker image"){
      //steps{
          //script{
            //docker.withRegistry('https://git.persistent.co.in:4567' , 'gitlab_cred'){
              //customImage = docker.build("git.persistent.co.in:4567/testgroup/springboot-docker-sample")
              //customImage.push()
            //}
          //}
      //}
    //}
 }

 post{
   success{
     slackSend (
        color: '#006400',
        message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
     )
   }
   failure{
     slackSend (
        color: '#8B0000',
        message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
     )
   }
 }
}