node {

    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }

    stage('Clone repository') {
        checkout scm
    }



    stage('Scan Function and Publish to Jenkins') {
        try {
            prismaCloudScanFunction cloudFormationTemplateFile: '', functionName: 'hello-word-python-rbc', functionPath: 'hello-word-python-rbc.zip', logLevel: 'info', project: '', resultsFile: 'prisma-cloud-scan-results.json'
        } finally {
            prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
        }
    }

    stage('Scan function with twistcli') {
        withCredentials([usernamePassword(credentialsId: 'twistlock_creds', passwordVariable: 'TL_PASS', usernameVariable: 'TL_USER')]) {
            sh 'curl -k -u $TL_USER:$TL_PASS --output ./twistcli https://$TL_CONSOLE/api/v1/util/twistcli'
            sh 'sudo chmod a+x ./twistcli'        
            sh './twistcli serverless scan --u $TL_USER --p $TL_PASS --address https://$TL_CONSOLE --details --publish lambda_jenkins_rbenavente_paloaltonetworks_com-masterssh-test.zip'
        } 
    }

        def TW_BASE64_POLICY = sh(script: "cat TW_BASE64_POLICY.json", returnStdout:true).trim()
        //println TW_BASE64_POLICY



    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }
}
