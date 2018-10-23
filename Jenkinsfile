pipeline{
  agent any
  
  stages {
    stage('Build Maven'){
      environment {
        mvnHome = tool 'M3'
      }
      steps {
        script {
          sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
          archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
          junit testResults: '**/target/surefire-reports/TEST-*.xml'
        }
      }
    }

    stage('output'){
      steps {
        version()
      }
    }
  }
}

@NonCPS  
void version() {
    def m = readFile('pom.xml') =~ '<version>(.+)</version>'
    if (m){
      echo "Building version ${m[0][1]}"
    }
}
