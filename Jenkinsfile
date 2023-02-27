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
    
    stage('User Acceptance Test - AuthService') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', description: '', name: 'Pass')]
	
	  if(response=="Yes") {

	    stage('Release- AuthService') {
	     sh 'gradle build -x test'
	     sh 'echo AuthService is ready to release!'

	    }
	  }
    }
}
