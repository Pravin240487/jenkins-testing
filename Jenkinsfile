pipeline {
    options
    {
        disableConcurrentBuilds()
        ansiColor('xterm')
        skipStagesAfterUnstable()
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '2'))
    }
    environment {
     TERRAFORM_VERSION = "0.14.10"
     PYTHON_VERSION = "3.6"
   }
    parameters
    {
        choice(
            choices:'nonprod',
            description:'Profile name',
            name:'profile')
        string(name: 'role', defaultValue: 'arn:aws:iam::165387667510:role/AWS_165387667510_Owner', description: 'What role should I use?')

    }
    agent
    {
        node {
        label 'docker-kitchensink-slave'
        }

    }
    stages
    {
        stage('Checkout')
        {
            steps
            {
                checkout scm
            }
        }
        stage('Configure AWS')
        {
            steps
            {
                script {
                    def credentialId = "aws-key"
                    withCredentials([usernamePassword(credentialsId: "${credentialId}", usernameVariable: 'USER', passwordVariable: 'PASS')])
                    {
                        sh """
                            echo "Hello World Pravin"
                        """
                    }
                }
            }
        }
        
    }
//terraform apply -input=false tfplan
//terraform destroy --auto-approve
    post
    {
        success
        {
            emailext (
                to: "psoundararajan@tonikbank.com",
                subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"""
            )
        }
        failure
        {
            emailext (
                to: "psoundararajan@tonikbank.com",
                subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """<p>FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"""
            )
        }
    }
}
