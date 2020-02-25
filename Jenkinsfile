//Jenkinsfile
node {
stage('Preparation') {
      //Installing kubectl in Jenkins agent
      sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/arm/kubectl'
  sh 'sudo chmod +x ./kubectl && mv kubectl /usr/bin'
//Clone git repository
  git url:'https://github.com/Otterwerks/kubernetes-jenkins-nginx.git'
   }
  
  //Test deploy only
stage('Integration') {
 
      withKubeConfig([credentialsId: 'jenkins-robot', serverUrl: 'https://192.168.11.24:6443']) {
      
         sh 'kubectl apply -f deployment.yaml'
        
      }                      
      
 }
}
