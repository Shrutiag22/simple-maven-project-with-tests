pipeline{
  agent any
  environment {
      mvnHome = tool 'M3'
      v = version()
  }
  stages {
    stage('Build Maven'){
      steps {
        script {
          if (v) {
          echo "Building version ${v}"
          }
        }
        
        sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
      }
    }
    
    stage('Archive artifacts'){
      steps{
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        junit testResults: '**/target/surefire-reports/TEST-*.xml'
        
        script {
          version() {
            matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
            matcher ? matcher[0][1] : null
          }
        }
      }
    }
  }
  
}
  
