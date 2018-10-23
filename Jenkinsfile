pipeline{
  agent any
  stages {
    stage('Build Maven'){
      steps {
        def mvnHome = tool 'M3'
        sh "${mvnHome}/bin/mvn -B verify"
      }
    }
  }
}
  
