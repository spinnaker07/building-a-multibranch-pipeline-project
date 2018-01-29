timestamps 
{
properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '1', artifactNumToKeepStr: '1', daysToKeepStr: '1', numToKeepStr: '1']]])

node () 
    {
    def repo = ["k2io/k2-agent", "k2io/k2-useragent-docker", "k2io/go-iptables", "emicklei/go-restful", "puerkitobio/purell", "golang/glog", "go-openapi/spec", "google/gofuzz", "bronze1man/goStrongswanVici", "docker/docker", "mailru/easyjson", "golang.org/x/sys/unix"]
    for (item in repo){
    stage ('Checkout '+item) 
        {
          dir("src/github.com/"+item) 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/'+item+'.git']]])
	 }
      }
    }
    def repo2 = ["golang.org/x/sys/unix", "k8s.io/client-go"]
    stage ('Checkout '+item) 
    {
    for (item in repo2){
          dir("src/"+item) 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://'+item+'.git']]])
	 }
        }    
    }
    stage ('K2-Zday-agent - Build') {
       sh """
       GOPATH='${env.WORKSPACE}'
       PATH='${env.PATH};/usr/local/bin/go'
       GOBIN='${env.GOPATH}/${env.BUILD_NUMBER}'
       image_name="k2cyber/rel-k2-zday-agent:${env.BUILD_NUMBER}"
       cd ${env.WORKSPACE}
       cp src/github.com/k2io/k2-agent/zdayserver/Dockerfile.ubuntu ${env.WORKSPACE}/Dockerfile
       docker build -t ${env.image_name} .
       docker push ${env.image_name}
       docker rmi ${env.image_name}
       """
      }
   }
}
