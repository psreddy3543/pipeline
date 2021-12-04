pipeline
{
    agent any
    stages
    {
     
     stage ('compile code')
     {
         steps
         {
             sh 'mvn install'
         }
     }
     stage ('test')
     {
         steps
         {
             sh 'mvn test'
         }
     }
     stage ('find my binary')
     {
         steps
         {
             sh 'find / -name *.war'
         }
     }
        stage ('increase versions')
        {
            steps
            {
             sh 'mvn -U versions:set -DnewVersion=${version}'
        }
    }
     stage ('deploy')
     {
         steps
         {
             sh 'cp -R /root/.jenkins/workspace/newpipe/target/* /opt/apache-tomcat-8.5.3/webapps'
         }
      }
        stage ('connect to s3')
         {
             steps
             {
               s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'papareddy3543/artifacts_storage/', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-2', showDirectlyInBrowser: false, sourceFile: '**/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'SUCCESS', profileName: 'reddy', userMetadata: []
             }
         }
     }
     post 
    {
        always 
        {
            slackSend channel: '#developer',                
                message: "Result : ${currentBuild.currentResult}\n Job : ${env.JOB_NAME}\n buildno : ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
          }
 {
           publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
          }    
    }
 }     
