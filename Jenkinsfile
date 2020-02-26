node {
      
    stage('Preparation') {
        git url:'https://github.com/Otterwerks/kubernetes-jenkins-nginx.git'
    }

    stage('Build') {
        sh 'docker build -t otterwerks/kubernetes-jenkins-nginx-demo .'
        sh 'docker push otterwerks/kubernetes-jenkins-nginx-demo' //requires once from kubernetes host node: docker exec -it <jenkins-container-id> bash, docker login
    }

    stage('Deploy') {
        withKubeConfig([credentialsId: 'jenkins-robot',
                        serverUrl: 'https://192.168.11.24:6443'
                       ]) {
                            sh 'kubectl apply -f deployment.yaml'
                       }                      
   }
      
}
