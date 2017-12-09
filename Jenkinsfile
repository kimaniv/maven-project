pipeline {
  agent any

  parameters {
    // Like variables here
    string(name: 'tomcat_dev', defaultValue: '34.207.67.102', description: 'Tomcat dev environment')
    string(name: 'tomcat_prod', defaultValue: '54.86.137.53', description: 'Tomcat prod environment')
  }

  triggers {
    //Cron here
    pollSCM('* * * * *')
  }

  stages {
    stage ('Build'){
      steps {
        sh '/usr/local/bin/mvn clean package'
      }
      post {
        success {
          echo 'Now Archiving...'
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }

    stage ('Deployments'){
      //Allow for parallel running of these
      parallel{
        stage ('Deploy to Staging'){
          steps {
            sh "scp -i /Users/edwardxie/.ssh/JenkinsKeyPair **/target/*.war ec2-user@${tomcat_dev}:/var/lib/tomcat7/webapps"
          }
        }

        stage ('Deploy to Production'){
          steps {
            sh "scp -i /users/edwardxie/.ssh/JenkinsKeyPair **/target/*.war ec2-user@${tomcat_prod}:/var/lib/tomcat7/webapps"
          }
        }
      }
    }
  }
}