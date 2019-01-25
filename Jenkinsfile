def userInput = true
def didTimeout = false
try {
    timeout(time: 15, unit: 'SECONDS') { 
        userInput = input(
        id: 'Proceed1', parameters: [
        [$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']
        ])
    }
} catch(err) { 
    def user = err.getCauses()[0].getUser()
    if('SYSTEM' == user.toString()) { 
        didTimeout = true
    } else {
        userInput = false
        echo "Aborted by: [${user}]"
    }
}




node(){
	env.CLAIR_IP="172.17.0.1"
    
	if (userInput == true){
		
	  cleanWs()
    stage ("CheckOut"){
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
        sh "clair-scanner_linux_amd64 --ip 172.17.0.1 -r report2.json benhall/elasticsearch:1.4.2"

    }
	
 
    
   
	
    
    
    stage("Incoming Webhook to Slack"){
	    sh "chmod 755 slack.sh"
	    sh "./slack.sh"
    }
	}
	else{
	 echo "Aborting"
        currentBuild.result = 'FAILURE'
	}
}
