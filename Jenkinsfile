node(){
    env.CLAIR_IP="172.17.0.1"
    
    cleanWs()
    stage("CheckOut"){
        checkout scm
    }
	
 
    
   // stage("Run clair-db"){
     //   sh "docker run -p 5433:5433 -d --name db5 arminc/clair-db:2017-10-17"
    //}

    //stage("Run postgres"){
      //  sh "docker run -p 6061:6061 --link db:postgres -d --name clair5 arminc/clair-local-scan:v2.0.1"
    //}
	
   // stage("Pull Docker Image"){
     //   sh "docker pull benhall/elasticsearch:1.4.2"
   // }

    stage("Docker Image Vulnerability Analysis"){
        sh "clair-scanner_linux_amd64 --ip 172.17.0.1 -r report.json ubuntu"

    }
    
    stage("Incoming Webhook to Slack"){
	sh " curl -X POST -d 'payload={"text":"Message to be displayed"}' https://hooks.slack.com/services/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"
	}
	
	
  
}
