pipeline {
       agent
    {
        node {
        label 'docker-kitchensink-slave'
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
