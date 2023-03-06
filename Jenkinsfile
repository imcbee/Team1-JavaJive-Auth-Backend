node {
    stage ("Checkout AuthService"){
        git branch: 'master', url: 'https://github.com/imcbee/Team1-JavaJive-Auth-Backend.git'
    }
    
    stage ("Gradle Build - AuthService") {
	
		sh 'gradle clean build' // replace all bat into sh for linux systems

    }
    
    stage ("Gradle Bootjar-Package - AuthService") {
        sh 'gradle bootjar'
    }
    
    stage ("Containerize the app-docker build - AuthApi") {
        sh 'docker build --rm -t mcc-auth:v1.0 .'
    }
    
    stage ("Inspect the docker image - AuthApi"){
        sh "docker images mcc-auth:v1.0"
        sh "docker inspect mcc-auth:v1.0"
    }
    
    stage ("Run Docker container instance - AuthApi"){
        sh "docker run -d --name mcc-auth -p 8081:8081 mcc-auth:v1.0"
     }
    
    stage('User Acceptance Test - AuthService') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {
	  
	    stage('Release - AuthService') {
	      sh 'docker stop mcc-auth'
	      sh 'echo MCC AuthService is ready to release!'
	    }
	  }
    }
}
