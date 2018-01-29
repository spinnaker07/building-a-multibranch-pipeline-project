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
        echo env.PATH
        echo env.BUILD_NUMBER
        echo env.WORKSPACE
        withEnv(GOPATH=env.WORKSPACE, PATH=env.PATH+'/usr/local/go/bin', GOBIN=env.GOPATH+"/"+env.BUILD_NUMBER)
        {
	def image_name="k2cyber/rel-k2-zday-agent:"env.BUILD_NUMBER
        echo image_name
        echo env.GOPATH
        echo env.WORKSPACE
        echo env.BUILD_NUMBER 
        sh 
        """	
       cd ${WORKSPACE}
	cp src/github.com/k2io/k2-agent/zdayserver/Dockerfile.ubuntu ${WORKSPACE}/Dockerfile
	docker build -t ${image_name} .
	docker push ${image_name}
	docker rmi ${image_name} 
	 """ 
	}
    }
    }
}
