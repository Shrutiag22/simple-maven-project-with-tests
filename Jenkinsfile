pipeline{
  agent any
  environment {
  mvnHome = tool 'M3'
  v = version()
    if (v) {
      echo "Building version ${v}"
    }
  }
  stages {
    stage('Build Maven'){
      steps {
        sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
      }
    }
    
    stage('Archive artifacts'){
      steps{
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        junit testResults: '**/target/surefire-reports/TEST-*.xml'
      }
    }
  }
  version() {
   matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
   matcher ? matcher[0][1] : null
  }
}
  
