#!/usr/bin/env groovy

def SESSION_NAME='First website'
properties([
  parameters([
  string(name: 'ENV',defaultValue:'',description:'env'),
  string(name: 'ACCOUNT',defaultValue:'',description:'aws account id'),
  text(name: 'REGION',defaultValue: 'TEXT',description: ''),
  booleanParam(name: 'BOOLEAN',defaultValue: true,description: ''),
  choice(name: 'PARAMETER',choices: ['string','text','booleanParam','choice','password'],description: ''),
  password(name: 'PASSWORD',defaultValue: '',description: '')
 ])
])
pipeline {
    agent {

         node { 
             label 'dind'
           }
         
         }
    triggers {
             cron('*/10 * * * *')
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
             stage ('print param'){
                steps{
                  echo "This is example of parameter ${params.REGION}"
                  echo "This is example of parameter ${params.BOOLEAN}"
                  echo "This is example of parameter ${params.CHOICE}"
                  echo "This is example of parameter ${params.PASSWORD}"
                  echo "This is example of parameter ${params.ENV}"
                 //     script {
                  //         build job:"first_website/main"
                     //       }
                     }
                 }
              stage('Input example')
               {
                input {
                     message " Should we cont?"
                     ok "Yes,we should"
                     submitter "sagar"
                     parameters {
                         string(name:'PERSON',defaultValue: 'Mr Jenkins', description:'Who should I say hello')
                      }
                    }
                     steps{
                         echo "Hello,${PERSON},nice to meet you."
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
