#!/usr/bin/env groovy

def SESSION_NAME='First website'
properties([
  parameters([
  string(name: 'ENV',defaultValue:'',description:'env'),
  string(name: 'ACCOUNT',defaultValue:'',description:'aws account id')
  text(name: 'TEXT',defaultValue:'param text',description: '')
  booleanParam(name: 'BOOLEAN',defaultValue:true,description: '')
  choice(name: 'PARAMETER',choices: [string,text,booleanParam,choice,password],description: '')
  password(name: 'PASSWORD',defaultValue: 'SECRET',description: '')
 ])
])
pipeline {
    agent {

         node { 
             label 'dind'
           }
         
         }
   options {
        timeout(time:360,unit: 'SECONDS')
        skipDefaultCheckout()
        timestamps()
    }
       environment {
         PASS = credentials('secret')
         TOKEN = credentials('token')
         USER = credentials ('username')
        }
       stages {
            stage ('checkout') {
              steps {
              script { echo 'checking out' 
              checkout scm}
              }
            }
            stage ('print envs'){
              steps {
                script {
                  sh 'echo "${ENV}"'
                  sh 'echo "$PASS"'
                  sh 'cat "$TOKEN"'
                  sh 'echo "Username: $USER_USR"'
                  sh 'echo "Password: $USER_PSW"'
                      }
                  }
              }
             stage ('print param')
                steps{
                  echo "This is example of parameter ${param.TEXT}"
                  echo "This is example of parameter ${param.BOOLEAN}"
                  echo "This is example of parameter ${param.CHOICE}"
                  echo "This is example of parameter ${param.PASSWORD}"
                  echo "This is example of parameter ${param.ENV}"
                     }
       }
  post { always {echo 'inside post for the always '}
  changed { echo 'Inside post fot the changed'}
  fixed { echo ' Inside post for the fixed'}
  regression {echo 'Only run the steps in post if the current Pipeline is failure,unstable,oraborted and previous run was successful'}
  aborted {echo 'If the current Pipeline run has an aborted' }
  failure {echo 'If current Pipeline or stage run has a failed '}
  success {echo 'If the current Pipeline or stage run has a success'}
  unstable {echo 'If the current Pipeline or stage run has a unstable'}
  unsuccessful {echo 'If the current Pipeline or stage run has not a success status'}
  cleanup {echo 'After evry other post condition has been evaluated'}
}

}
