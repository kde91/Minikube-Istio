pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        }

    stages {
    
        stage('Git') {
            steps {
               
                    git clone https://github.com/kde91/Minikube-Istio.git
                
            }
        }
		
		stage('Deploy Blue Container') {
            steps {
               
                   kubectl apply -f blue.yaml
                
            }
        }
		
		stage('Deploy Green Container') {
            steps {
               
                    kubectl apply -f green.yaml
                
            }
        }
		
		stage('Create Service for blue container') {
            steps {
               
                    kubectl apply -f svc-blue-green.yaml
                
            }
        }
	    
	    stage('Check deployment for blue container') {
            steps {
               
                    curl http://172.31.14.105:31562
                
            }
        }
	    
	    stage('Switch traffic for green container') {
            steps {
               
                    kubectl replace -f svc-blue-green.yaml
                
            }
        }
		
	}

}	
