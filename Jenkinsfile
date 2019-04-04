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
 }
}