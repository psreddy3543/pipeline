pipeline
{
    agent any 
   
    stages
    {
     
     stage ('compile code')
     {
         steps
         {
             sh 'mvn clean install'
         }
     }
     stage ('test')
     {
         steps
         {
             sh 'mvn test'
         }
     }
    
     stage ('deploy')
     {
         steps
         {
             sh 'cp -R /root/.jenkins/workspace/pipeline/target/* /opt/apache-tomcat-8.5.3/webapps'
         }
     }
    stage ('connect to S3')
        {
            steps
            {
           s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'papareddy3543/artifacts_storage/', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-2', showDirectlyInBrowser: false, sourceFile: '**/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'reddy', userMetadata: []    
            }   
        }
    }    
      post 
    {
        always
        {
            slackSend channel: '#jenkins',                
                message: "${currentBuild.currentResult}\n Job ${env.JOB_NAME}\n build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
        }
    }   
}
