timestamps 
{
node () 
    {
    stage ('K2-Zday-agent - Checkout') 
        {
         dir("src/github.com/k2io/k2-agent") 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/k2io/k2-agent.git']]])
	 }
        dir("src/github.com/k2io/k2-useragent-docker") 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/k2io/k2-useragent-docker.git']]])
	 }
       dir("src/github.com/k2io/go-iptables.git") 
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/k2io/go-iptables.git']]])
	 }
dir("src/github.com/emicklei/go-restful")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/emicklei/go-restful.git']]])
	 }
dir("src/github.com/PuerkitoBio/purell.git")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/PuerkitoBio/purell.git']]])
	 }
dir("src/github.com/golang/glog")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/golang/glog.git']]])
	 }

dir("src/github.com/go-openapi/spec")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/go-openapi/spec.git']]])
	 }

dir("src/github.com/google/gofuzz")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/google/gofuzz.git']]])
	 }
dir("src/github.com/goStrongswanVici")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/bronze1man/goStrongswanVici.git']]])
	 }
dir("src/github.com/docker/docker")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/docker/docker.git']]])
	 }
dir("src/github.com/mailru")
          {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/mailru/easyjson.git']]])
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
