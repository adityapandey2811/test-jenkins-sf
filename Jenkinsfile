pipeline {
    agent any

    stages {
        stage('Fetch Code') {
            steps {
                // Checkout code from GitHub using token authentication
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'CleanBeforeCheckout']],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/adityapandey2811/test-jenkins-sf.git',
                                               credentialsId: 'github-tkn']]])
            }
        }
        stage('Run Tests') {
            steps {
                // Authenticate with your Salesforce development org
                bat 'sfdx force:auth:jwt:grant --clientid 3MVG9pRzvMkjMb6nuaDwq1YNacTuPNITGteqqF0TILP6cyBvxqBPYmFvSsA8SrYOtqBuTmabDIQatBxpSu5Ym --jwtkeyfile C:/Users/adity/JWT/server.key --username 	chhenatoast@resilient-moose-d303ud.com --setdefaultdevhubusername -a MyDevOrg'
        
                // Run Apex tests
                bat 'sfdx force:apex:test:run -u MyDevOrg -w 1'
        
                // Perform static code analysis using PMD
                bat 'sfdx force:pmd:check -u MyDevOrg'
            }
        }
        stage('Package') {
            steps {
                // Create a deployable package with Salesforce DX CLI
                bat 'sfdx force:package:create -u MyDevOrg -p MyPackage -v 1.0.0'
            }
        }
        
    }
}
