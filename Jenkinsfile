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
                      }
                  }
              }
       }
  post { always {echo 'inside post for the always '}
  changed { echo 'Inside post fot the changed'}
  fixed { echo ' Inside post for the fixed'}
  regression {echo 'Only run the steps in post if the current Pipeline is failure,unstable,oraborted and previous run was successful'}
       }
}
