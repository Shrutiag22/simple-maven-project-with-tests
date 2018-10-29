pipeline{
  agent any
  
  stages {
    stage('Build Maven'){
      environment {
        mvnHome = tool 'M3'
      }
      steps {
        script {
          sh "${mvnHome}/bin/mvn -B verify" 
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

    stage('Example'){
      steps{
        echo "Running ${env.BUILD_ID} on ${env.JOB_NAME}"
      }
    }

    stage('output'){
      steps {
        version(readFile('pom.xml'))
      }
    }
  }

  post{
    always{
      junit testResults: '**/target/surefire-reports/TEST-*.xml'
    }
  }
}

@NonCPS  
void version(text) {
    def m = text =~ '<version>(.+)</version>'
    echo "Building version ${m[0][1]}"
}
