node{
   stage('SCM Checkout'){
     git 'https://github.com/vedantek/java-maven-war'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   stage('Slack Notification'){
       slackSend baseUrl: 'https://hooks.slack.com/services/',
       channel: '#cicd-b02',
       color: 'good', 
       message: 'Welcome to Jenkins, Slack!', 
       teamDomain: 'vedantek',
       tokenCredentialId: 'slack'
   }
}
