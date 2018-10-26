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
        }
      }
    }

    stage('Deploy'){
      when {
        expression {
          currentBuild.result == null || currentBuild.result == 'SUCCESS'
        }
      }
      steps{
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
      }
    }

    stage('Test'){
      steps{
        junit testResults: '**/target/surefire-reports/TEST-*.xml'
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
    echo "Building version ${m[0][1]}"
}
