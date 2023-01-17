#!/usr/bin/env groovy

def SESSION_NAME='First website'
properties([
  parameters([
  string(name: 'ENV',defaultValue:'',description:'env'),
  string(name: 'ACCOUNT',defaultValue:'',description:'aws account id')
    ])
])
pipeline {
    agent {

         node { 
             label 'dind'
           }
         
         }
   options {
        skipDefaultCheckout()
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
                  sh("echo '${ENV}'")
                  sh("echo $PASS")
                  sh("cat $TOKEN")
                  sh("Username: $USER_USR")
                  sh("Password: $USER_PSW")
                      }
                  }
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
