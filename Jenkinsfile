timestamps 
{
node () 
    {
    stage ('K2-Zday-agent - Checkout') 
        { 
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanCheckout']], userRemoteConfigs: [[ credentialsId: '07', url: 'https://spinnaker07@github.com/k2io/k2-agent.git']]])
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
