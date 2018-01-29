timestamps 
{
node () 
    {
    def repo = ["k2io/k2-agent", "k2io/k2-useragent-docker", "k2io/go-iptables", "emicklei/go-restful", "puerkitobio/purell", "golang/glog", "go-openapi/spec", "google/gofuzz", "bronze1man/goStrongswanVici", "docker/docker", "mailru/easyjson"]
    for (item in repo){
    stage ('Checkout '+item) 
        {
          dir("src/github.com/"+item) 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/'+item+'.git']]])
	 }
}
        
}
    stage ('K2-Zday-agent - Build') {
    // Shell build step
	sh """ 
	export PATH=$PATH:/usr/local/go/bin/
	export GOPATH=${WORKSPACE}
	export GOBIN=${WORKSPACE}/${BUILD_NUMBER}
	image_name=k2cyber/rel-k2-zday-agent:${BUILD_NUMBER}
	cd ${WORKSPACE}
	cp src/github.com/k2io/k2-agent/zdayserver/Dockerfile.ubuntu ${WORKSPACE}/Dockerfile
	docker build -t ${image_name} .
	docker push ${image_name}
	docker rmi ${image_name} 
	 """ 
	}
    }
}
