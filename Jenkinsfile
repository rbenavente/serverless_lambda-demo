node {

    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }

    stage('Clone repository') {
        checkout scm
    }

    stage('Zip lambda  Function') {
     zip dir: './code', glob: '', zipFile: 'myFunction.zip'
        
    }
    
// You can scan functions using one of these methods: Prisma Cloud Jenkins plugin or twiscli. 

    stage('Scan Function and Publish to Jenkins') {
        try {
            prismaCloudScanFunction cloudFormationTemplateFile: '', functionName: 'myFunction', functionPath: 'myFunction.zip', logLevel: 'info', project: '', resultsFile: 'prisma-cloud-scan-results.json'
        } finally {
            prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
        }
    }

    // twistcli only when Jenkins plugin is not installed 
    stage('Scan function with twistcli') {
        withCredentials([usernamePassword(credentialsId: 'twistlock_creds', passwordVariable: 'TL_PASS', usernameVariable: 'TL_USER')]) {
            sh 'curl -k -u $TL_USER:$TL_PASS --output ./twistcli https://$TL_CONSOLE/api/v1/util/twistcli'
            sh 'sudo chmod a+x ./twistcli'        
            sh './twistcli serverless scan --u $TL_USER --p $TL_PASS --address https://$TL_CONSOLE --details --publish myFunction.zip'
        } 
    }

        def TW_BASE64_POLICY = sh(script: "cat TW_BASE64_POLICY.json", returnStdout:true).trim()
        //println TW_BASE64_POLICY



    stage('Clean') {
        sh 'rm * -f -r -d -v'
    }
}
