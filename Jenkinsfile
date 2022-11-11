#!/usr/bin/env groovy

def SESSION_NAME='First website'
properties([
  parameters([
  string(name: 'ENV',defaultValue:'',description:'env'),
  string(account: ACCOUNT,defaultValue:'',description:'aws account id')
    ])
])
pipeline {
    agent {
        docker {
            image 'centos:latest'
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
                  echo '${ENV}'
                  echo '${ACCOUNT}'
                      }
                  }
              }
       }
}
