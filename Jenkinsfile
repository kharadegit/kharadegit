#!/usr/bin/env groovy
pipeline {
    agent none
    stages {
       stage('No Sequential Stage'){
        agent {
            label 'dind'
         }
        steps {
           echo "On non sequential stage"
        }
      }
      stage("Sequential"){
         agent{
             label 'dind'
         }
         environment {
            FOR_SEQUENTIAL = "sequential pipeline"
         }
         stages {
             stage ('Sequentail 1'){
                  steps {
                     echo "In sequential one"
                   }
             }
             stage ('Sequentail 2'){
                  steps {
                     echo "In sequential two"
                   }
             }
             stage ('Parralel In sequential'){
                   parallel{
                       stage('In parallel one'){
                          steps {
                             echo "In sequential one"
                           }
                       }
                       stage('In parallel two'){
                          steps {
                             echo "In sequential two"
                           }
                       }  
                    }
                }
           }
       }
    }
}
