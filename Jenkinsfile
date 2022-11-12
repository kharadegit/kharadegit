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
        docker {
            image 'ubuntu:14.04'
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
}
