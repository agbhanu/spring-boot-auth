def customImage
pipeline{
 agent{
     docker{
       image 'blockchain_rnd/poc/corda/tradefinance/gradle-libltdl7:latest'
       registryUrl 'https://git.persistent.co.in:4567'
       registryCredentialsId 'siddhesh_creds'
       args '-v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock'
       //image 'gradle:jdk8-slim'
     }
 }
 stages{



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

    stage("Build docker image"){
      steps{
        sh "docker build -t 10.244.48.72:8123/spring-boot-auth ."
        sh "docker tag 10.244.48.72:8123/spring-boot-auth 10.244.48.72:8123/spring-boot-auth:${env.BUILD_NUMBER}"
      }
    }

    stage("Push docker image to nexus"){
      steps{
         withDockerRegistry([credentialsId: 'nexus_cred', url: 'http://10.244.48.72:8123']) {
            sh "docker push 10.244.48.72:8123/spring-boot-auth"
         }
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