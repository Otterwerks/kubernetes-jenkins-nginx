pipeline {

    agent any
    
    stages {
      
		stage('Preparation') {
			steps {
				git url:'https://github.com/Otterwerks/kubernetes-jenkins-nginx.git'
			}
		}

		stage('Build') {
			steps {
				sh 'docker build -t otterwerks/kubernetes-jenkins-nginx-demo .'
				 withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                        sh 'docker push otterwerks/kubernetes-jenkins-nginx-demo'
                    }
			}
		}

		stage('Deploy') {
			steps {
				withKubeConfig([credentialsId: 'jenkins-robot-global',
								serverUrl: 'https://192.168.11.24:6443'
								]) {
									sh 'kubectl apply -f deployment.yaml'
								}                      
			}
	    }
   
   }
      
}
