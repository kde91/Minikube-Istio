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
		
		stage('Create Service') {
            steps {
               
                    kubectl apply -f svc-blue-green.yaml
                
            }
        }
		
	}

}	
