pipeline {
    agent any

    environment {
        SFDX_CLI_EXECUTABLE = 'sfdx' // Specify the Salesforce CLI executable
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Authenticate with Salesforce') {
            steps {
                script {
                    // withCredentials([usernamePassword(credentialsId: 'salesforce-creds', passwordVariable: 'SFDC_PASSWORD', usernameVariable: 'SFDC_USERNAME')]) {
                        // Change to the Salesforce DX project directory
                        dir('C:/Users/adity/sf-md/MyProject') {
                            // Authenticate using JWT flow
                            bat "${SFDX_CLI_EXECUTABLE} force:auth:jwt:grant -i 3MVG9pRzvMkjMb6nuaDwq1YNacTuPNITGteqqF0TILP6cyBvxqBPYmFvSsA8SrYOtqBuTmabDIQatBxpSu5Ym -f C:/Users/adity/JWT/server.key --username chhenatoast@resilient-moose-d303ud.com -d -a MyDevOrg"
                        }
                    // }
                }
            }
        }

        stage('Validate Deployment') {
            steps {
                // Deploy metadata (replace with the appropriate command)
                bat "${SFDX_CLI_EXECUTABLE} force:source:deploy -p force-app -u MyDevOrg"
            }
        }

        stage('Manual Deployment') {
            steps {
                input(message: 'Approve deployment?', ok: 'Deploy')
                // Perform manual deployment (replace with the appropriate command)
                bat "${SFDX_CLI_EXECUTABLE} force:source:deploy -p force-app -u MyDevOrg"
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Finished!'
        }
    }
}
