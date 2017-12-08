pipeline {
  agent any

  stages {
    stage('Build'){
      steps {
        // Because I'm too lazy to set a path parameter...
        sh '/usr/local/bin/mvn clean package'
      }

      post {
        success {
          echo 'Now Archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }

    stage ('Deploy to Staging'){
      steps {
        build job: 'Deploy-to-staging'
      }
    }
  }
}