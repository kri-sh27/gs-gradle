// node {
//   def myGradleContainer = docker.image('gradle:jdk8-alpine')
//   myGradleContainer.pull()
//   stage('prep') {
//     checkout scm
//   }
//   stage('test') {
//      myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
//        sh 'cd complete && gradle test'
//      }
//   }
//   stage('run') {
//      myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
//        sh 'cd complete && gradle run'
//      }
//   }
// }

node {
  // Add a stage to install Docker
  stage('Install Docker') {
    sh 'sudo apt-get update'
    sh 'sudo apt-get install -y docker.io'
  }

  // Define and pull the Gradle Docker image
  def myGradleContainer = docker.image('gradle:jdk8-alpine')
  myGradleContainer.pull()

  stage('prep') {
    checkout scm
  }

  stage('test') {
    myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
      sh 'cd complete && gradle test'
    }
  }

  stage('run') {
    myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
      sh 'cd complete && gradle run'
    }
  }
}
