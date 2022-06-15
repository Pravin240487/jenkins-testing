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
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'aws-key') {
                  sh 'echo "Uploading content with AWS creds"'
                      AWS("--region=us-east-1 s3 ls")
                  }
              }
         }
     }
}
