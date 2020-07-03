pipeline {
    agent any
     stages {
         stage('Sonarqube') {
           environment {
                scannerHome = tool 'SonarScanner'
                }
         steps {
            withSonarQubeEnv('sonar') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
            timeout(time: 5, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
            }
          }
         }
     stage('Deploy') { 
           steps {
             sh ''' #! /bin/bash 
             
              aws deploy create-deployment --application-name ChatApp --deployment-group-name ChatAppDeploymentGroupCF --deployment-config-name CodeDeployDefault.AllAtOnce --github-location repository=Shashanksingh17/new_chatapp,commitId=${GIT_COMMIT}
             '''
                 }
               }
             }
           }
