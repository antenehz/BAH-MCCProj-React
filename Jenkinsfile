node {
    
    stage ("Checkout React Client"){
        git branch: 'main', url: 'https://github.com/abarbuzza/BAH-MCCProj-React.git'
    }
    
    stage ("Install dependencies - React Client") {
        sh 'npm install'
    }
    
    stage ("Containerize the app-docker build") {
        sh 'docker build --rm -t event-reactclient:v1.0 .'
    }
    
    stage ("Inspect the docker image"){
        sh "docker images event-reactclient:v1.0"
        sh "docker inspect event-reactclient:v1.0"
    }
    
    stage ("Run Docker container instance"){
	sh "docker stop event-reactclient"
        sh "docker run -d --rm --name event-reactclient -p 3000:3000 event-reactclient:v1.0"
    }
    
    stage('User Acceptance Test') {
	
	  def response= input message: 'Is this build good to go?',
	   parameters: [choice(choices: 'Yes\nNo', 
	   description: '', name: 'Pass')]
	
	  if(response=="Yes") {
	    stage('Deploy to Kubenetes cluster') {
	      sh "kubectl delete service event-reactclient"
	      sh "kubectl delete deployment event-reactclient"
	      sh "kubectl create deployment event-reactclient --image=event-reactclient:v1.0"
	      sh "kubectl expose deployment event-reactclient --type=LoadBalancer --port=80"
	    }
	  }
    }
    
    stage("Production Deployment View"){
        sh "kubectl get deployments"
        sh "kubectl get pods"
        sh "kubectl get services"
    }
}
