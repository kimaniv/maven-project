pipeline {
  agent any

  stage {
    stage('Build'){
      steps {
        sh 'mvn clean package'
      }

      post {

        //This is a conditional
        success {
          echo 'Now Archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
  }
}