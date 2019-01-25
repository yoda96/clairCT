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
        sh "clair-scanner_linux_amd64 --ip 172.17.0.1 -r report2.json alpine:3.5"

    }
    
    
    stage("Incoming Webhook to Slack"){
	    sh "chmod 755 slack.sh"
	    sh "./slack.sh"
    }
  
}
