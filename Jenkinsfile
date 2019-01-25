

node {

env.CLAIR_IP="172.17.0.1"
	  cleanWs()
    stage ("CheckOut"){
        checkout scm
    }


try {
	
    stage("Docker Image Vulnerability Analysis"){
        sh "clair-scanner_linux_amd64 --ip 172.17.0.1 -r report2.json alpine:3.5"

    }
	
          }
          catch(exception) {
           error "Image has vulnerabilities"
          }
          finally {
           step([$class: 'Publisher', reportFilenamePattern: 'test/automation/**/**/testng-results.xml'])
           // emailext attachLog: true, to: 'anshul.patel@infostretch.com'
           emailext body: '${FILE,path="test/automation/target/surefire-reports/emailable-report.html"}',
           mimeType: 'text/html', subject: 'Smoke Report: ${JOB_NAME} - ${BUILD_NUMBER}', 
           attachmentsPattern: 'test/automation/target/surefire-reports/emailable-report.html',
           to: 'dnyaneshwar.mundhe@infostretch.com'

           slackSend baseUrl: 'https://hooks.slack.com/services/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', 
           // channel: '#continuoustesting', 
            message: """Demo: Continuous Testing
            Clair Scanning: ${JOB_NAME} - ${BUILD_NUMBER}.
            For report, please visit <${BUILD_URL}/execution/node/7/ws/test/automation/target/surefire-reports/emailable-report.html|url>.""",
            tokenCredentialId: 'Slack_Continuous_Testing_Token'

              sh "python test-result-updater.py localhost 9200"

              input 'Please press proceed to continue to next stage'
                    
                }                
            }

}








