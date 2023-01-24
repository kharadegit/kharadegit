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
             cron('*/50 * * * *')
             }
   options {
        timeout(time:1089,unit: 'SECONDS')
        skipDefaultCheckout()
        buildDicarder(logRotator(numToKeepStr: '10'))
        timestamps()
    }
       environment {
         PASS = credentials('secret')
         TOKEN = credentials('token')
         USER = credentials ('username')
         DEPLOY_TO = 'dev'
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
                     }
                 }
              stage ('Example of sqeuntial pipeline')
              {
              steps{
                    script {
                       build job:"first_website/Sequential"
                     }
                   }
              }
              stage ('Example of Parallel pipeline')
              {
              steps{
                    script {
                       build job:"first_website/parallel"
                     }
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
              stage('when example single cond.')
              {
               when {branch 'dev' }
               steps{ echo 'Deploying dev using when single condition'}
              }
              stage('when example multiple cond.')
              {
               when {branch 'dev'
                     environment name:'DEPLOY_TO', value: 'dev'}
               steps{ echo "Deploying dev using when with multiple condition ${DEPLOY_TO}"}
               }
              stage('when example nested cond(allOf).')
              {
               when {
                     allOf{branch 'dev'
                     environment name:'DEPLOY_TO', value: 'dev'}}
               steps{ echo "Deploying dev using when condition allOf ${DEPLOY_TO}"}
               } 
               stage('when example multiple cond and nested cond.')
              {
               when {
                     branch 'dev'
                     anyOf{environment name:'DEPLOY_TO', value: 'dev'
                     environment name:'DEPLOY_TO', value: 'prod'}}
               steps{ echo "Deploying dev using when condition anyOf ${DEPLOY_TO}"}
               }
               stage('when example expression cond and nested cond.')
              {
               when {
                     expression { BRANCH_NAME ==~ /(dev|stage)/}
                     anyOf{environment name:'DEPLOY_TO', value: 'dev'
                     environment name:'DEPLOY_TO', value: 'stage'}}
               steps{ echo "Deploying dev using when condition expression ${DEPLOY_TO}"}
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
