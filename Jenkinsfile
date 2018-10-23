pipeline{
  agent any
  
  stages {
    stage('Build Maven'){
      environment {
        mvnHome = tool 'M3'
        def v = version()
      }
      steps {
        script {
          if (v) {
          echo "Building version ${v}"
          }
          sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
          archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
          junit testResults: '**/target/surefire-reports/TEST-*.xml'
          version() {
            matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
            matcher ? matcher[0][1] : null
          }
        }
      }
    }
  }
}
