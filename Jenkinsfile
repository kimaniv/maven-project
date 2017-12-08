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
    
    stage ('Deploy to Production'){
      steps{
        timeout(time:5, unit:'Days'){
          input message: 'Approve PRODUCTION Deployment?'
        }

        //This builds and deploys to prod if someone hits yes
        build job: 'Deploy-to-Prod'
      }

      // In response to the build
      post {
        success {
          echo 'Code deployed to Production.'
        }

        failure {
          echo 'Deployment failed.'
        }
      }
    }
  }
}