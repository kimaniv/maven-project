pipeline {
  agent any

  stage {
    stage('Build'){
      steps {
        sh 'mvn clean package'
      }

      post {
        success {
          echo 'Now Archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
  }
}