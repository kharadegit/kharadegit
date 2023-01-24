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
              if (fileExists('$CURRENT_DIR/test_build/hello.sh'))
              {
                    readFile('hello.sh')
               }
               else
                {
                    writeFile(file:'/var/jenkins_home/workspace/first_website_basic_steps/test_build/hello.sh',text:'Hello,Sagar')
                    readFile(file:'/var/jenkins_home/workspace/first_website_basic_steps/test_build/hello.sh')
                }
             }
         }
        
            post {
                 always{
                    sleep(time: 10)
                    deleteDir()
                    }
                 }
            
       }
    }
}
