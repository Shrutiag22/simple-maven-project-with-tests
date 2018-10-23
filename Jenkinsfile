pipeline{
  agent any
  environment {
  mvnHome = tool 'M3'
}
  stages {
    stage('Build Maven'){
      steps {
        sh "${mvnHome}/bin/mvn -B verify"
      }
    }
  }
}
  
