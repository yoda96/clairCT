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
	      
    stage("Incoming Webhook to Slack"){
	    sh "chmod 755 slack.sh"
	    sh "./slack.sh"
    }
	
    } catch(err) {
       
        throw err
    }

    stage "deploy"

    echo "Im deploying now!"
}








