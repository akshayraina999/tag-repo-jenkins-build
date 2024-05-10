pipeline {
     agent any

     tools {nodejs "Node16"}
     stages{
       stage('checkout'){
            steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://gitlab.com/imanishchaudhary/simple-node-js-react-npm-app.git']]])
        }
        }
            stage("Build") {
            steps {
      
             /*   slackSend channel: '#pipeline', color: '#439FE0', message: "For ${env.tags} tag, The build process has started. Job Name:-${env.JOB_NAME} Build No.:-${env.BUILD_NUMBER}, For logs click <${env.BUILD_URL}|here>", teamDomain: 'jenkins-scy4932', tokenCredentialId: '23b64830-463e-4bcd-9d4d-4af0fa266eb7', username: 'Jenkinsss'
         */
               echo "Building now"
                sh "npm install"
                
            }
        }                
            
        stage("Deploy to AUS") {
             when { tag "*-aus" }

          

             steps{ 
               sh "npm run build"
                echo "Creating the Zip File"
                sh "tar -czvf ${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz build/*"
          
withAWS(region: 'us-east-1') {
    s3Upload(file:"${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz", bucket:'artifactoryjenkins') 
}
                  

            /*   slackSend channel: '#pipeline', color: '#99FF99', message: "Click <${env.BUILD_URL}input|here> to Approve or Abort the deployment to AUS or click here to <${env.BUILD_URL}console|see logs>", teamDomain: 'jenkins-scy4932', tokenCredentialId: '23b64830-463e-4bcd-9d4d-4af0fa266eb7', username: 'Jenkinsss'
               mail to: 'imchaudhary101@gmail.com', subject: "Please approve #${env.BUILD_NUMBER}", body: "to Approve or Abort the deployment to AUS, click on the link ${env.BUILD_URL}input or for more info please click here ${env.BUILD_URL}console"
               input "Ready to deploy for AUS Server ?"
                    echo "deploying to AUS"  */
                    
                 }
                 
                 

                   /* sshPublisher(publishers: [sshPublisherDesc(configName: 'bastion', 
                    transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, 
                    makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/var/www/html', remoteDirectorySDF: false, removePrefix: '/build', 
                    sourceFiles: 'build/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                    */ }

             stage("Deploy to EU") {
             when { tag "*-eu"}

             steps{
               sh "npm run build"
                echo "Creating the Zip File"
                sh "tar -czvf ${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz build/*"
           /*     sh "curl -v --user 'admin:xxx' --upload-file build.tar.gz http://13.234.78.160:8081/repository/BUILD_USA/build_${JOB_NAME}_${BUILD_NUMBER}.tar.gz" */
           withAWS(region: 'us-east-1') {
    s3Upload(file:"${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz", bucket:'artifactoryjenkins') 
}
  
   
              
               /* slackSend channel: '#pipeline', color: '#99FF99', message: "Click <${env.BUILD_URL}input|here> to Approve or Abort the deployment to EU or click here to <${env.BUILD_URL}console|see logs>", teamDomain: 'jenkins-scy4932', tokenCredentialId: '23b64830-463e-4bcd-9d4d-4af0fa266eb7', username: 'Jenkinsss'
               mail to: 'imchaudhary101@gmail.com', subject: "Please approve #${env.BUILD_NUMBER}", body: "to Approve or Abort the deployment to EU, click on the link ${env.BUILD_URL}input or for more info please click here ${env.BUILD_URL}console" 
               input "Ready to deploy for EU Server ?"
                    echo "deploying to EU" */
             }
                 
                 
                 

                   /* sshPublisher(publishers: [sshPublisherDesc(configName: 'bastion', 
                    transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, 
                    makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/var/www/html', remoteDirectorySDF: false, removePrefix: '/build', 
                    sourceFiles: 'build/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                    */ }

             stage("Deploy to USA") {
              
             when { 
                tag  "*-us"}  
                    
              steps{ 
                sh "npm run build"
                echo "Creating the Zip File"
                sh "tar -czvf ${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz build/*"
              /*  sh "curl -v --user 'admin:shadypark' --upload-file build.tar.gz http://13.234.78.160:8081/repository/BUILD_USA/build_${JOB_NAME}_${BUILD_NUMBER}.tar.gz" */
              withAWS(region: 'us-east-1') {
    s3Upload(file:"${env.JOB_BASE_NAME}_${env.BUILD_NUMBER}.tar.gz", bucket:'artifactoryjenkins') 
}
  
   

          /*     slackSend channel: '#pipeline', color: '#99FF99', message: "Click <${env.BUILD_URL}input|here> to Approve or Abort the deployment to USA or click here to <${env.BUILD_URL}console|see logs>", teamDomain: 'jenkins-scy4932', tokenCredentialId: '23b64830-463e-4bcd-9d4d-4af0fa266eb7', username: 'Jenkinsss'
               mail to: 'imchaudhary101@gmail.com', subject: "Please approve ${env.BUILD_NUMBER}", body: "to Approve or Abort the deployment to USA, click on the link ${env.BUILD_URL}input or for more info please click here ${env.BUILD_URL}console"
               input "Ready to deploy for USA Server ?"
               echo "deploying to USA"
               sshagent(['manishnewnew']) {
                    sh ''' scp -o StrictHostKeyChecking=no -r build/* ubuntu@13.127.226.80:/var/www/jenkins-react-app '''
*/
}
                    
                 }
                 
                  }

}
