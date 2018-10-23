pipeline{
  agent any
  environment {
  mvnHome = tool 'M3'
}
  stages {
    stage('Build Maven'){
      steps {
        sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
      }
      input {
        message 'Ready to go?'
      }
    }
    
    stage('Archive artifacts'){
      steps{
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        junit testResults: '**/target/surefire-reports/TEST-*.xml'
      }
    }
  }
}
  
