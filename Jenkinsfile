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
        version(readFile('pom.xml'))
      }
    }
  }
}

@NonCPS  
void version(text) {
    def m = text =~ '<version>(.+)</version>'
    m ? m[0][1] : null
    echo "Building version ${m}"
}
