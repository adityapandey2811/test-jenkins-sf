pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Authenticate with Salesforce') {
            steps {
                // script {
                //     withCredentials([usernamePassword(credentialsId: 'salesforce-creds', passwordVariable: 'SFDC_PASSWORD', usernameVariable: 'SFDC_USERNAME')]) {
                //         bat '''
                //         sf login --instanceurl https://login.salesforce.com --clientid YOUR_CONSUMER_KEY --clientsecret YOUR_CONSUMER_SECRET --username $SFDC_USERNAME --password $SFDC_PASSWORD
                //         '''
                //     }
                // }
                bat 'cd C:/Users/adity/sf-md/MyProject'
                bat 'sfdx force:auth:jwt:grant -i 3MVG9pRzvMkjMb6nuaDwq1YNacTuPNITGteqqF0TILP6cyBvxqBPYmFvSsA8SrYOtqBuTmabDIQatBxpSu5Ym -f C:/Users/adity/JWT/server.key --username chhenatoast@resilient-moose-d303ud.com -d -a MyDevOrg'
            }
        }

        stage('Validate Deployment') {
            steps {
                bat 'sf deploy metadata preview -d C:/Users/adity/sf-md/MyProject'
            }
        }

        stage('Manual Deployment') {
            steps {
                input(message: 'Approve deployment?', ok: 'Deploy')
                bat 'sf deploy metadata -d C:/Users/adity/sf-md/MyProject'
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Finished!'
        }
    }
}
