node{
   stage('SCM Checkout'){
     git 'https://github.com/vedantek/java-maven-war'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   stage('Slack Notification'){
       slackSend baseUrl: 'https://hooks.slack.com/services/',
       channel: '#cicd-b03',
       color: 'good', 
       message: 'Jenkins Build Success!', 
       teamDomain: 'vedantek',
       tokenCredentialId: 'slack'
   }
   stage('Upload to S3'){
   s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'vini-firstlab', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: 'target/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 's3-full', userMetadata: []
   }
   
   stage('Deploy to Tomcat'){
   
    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.235.245.245/var/lib/tomcat9/webapps/'
   
   }
   stage('Slack Notification'){
       slackSend baseUrl: 'https://hooks.slack.com/services/',
       channel: '#cicd-b03',
       color: 'good', 
       message: 'Package is uploaded to S3!', 
       teamDomain: 'vedantek',
       tokenCredentialId: 'slack'
   }
}
