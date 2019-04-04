pipeline{
 agent{
   docker{
     image 'gradle:jdk8-slim'
   }
 }
 stages{
    stage('Initialize'){
      script{
      def dockerHome = tool 'Docker'
      env.PATH = "${dockerHome}/bin:${env.PATH}"
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