pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
//         stage('Security Scan') {
//              steps { 
//                 aquaMicroscanner imageName: 'alpine:latest', notCompleted: 'exit 1', onDisallowed: 'fail'
//              }
//         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'eu-central-1',credentials:'79dba0eb-1699-4fde-8296-dfb1165043ee') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'rieck-andre-static-jenkins-pipeline')
                  }
              }
         }
     }
}
