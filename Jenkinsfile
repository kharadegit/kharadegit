#!/usr/bin/env groovy


pipeline {
    agent {
         node { 
             label 'dind'
           }
         }
   options {
        timeout(time:1089,unit: 'SECONDS')
        skipDefaultCheckout()
        buildDiscarder(logRotator(numToKeepStr: '1'))
        timestamps()
    }
    
    stages {
      stage('Example of basics') {
        steps{
         script{
           //   withEnv([CURRENT_DIR="test"])
           //     {
           def C_PWD = pwd()
           sh 'mkdir test_build'
           dir('test_build'){sh 'pwd'}
           echo 'directory created'
              if (fileExsist('$CURRENT_DIR/test_build/hello.sh'))
              {
                    readFile('hello.sh')
               }
               else
                {
                    writeFile(file:'hello.sh',text:'Hello,Sagar')
                }
             }
         }
        
            post {
                 always{
                    deleteDir("${C_PWD}")
                    }
                 }
            
       }
    }
}
