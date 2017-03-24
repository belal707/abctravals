node 
{
  	checkout scm
  	stage('Package') 
  	{
     	sh 'mvn clean package -DskipTests'
  	}
	stage('Create Docker Image') 
	{
			docker.build("belalansari/abctravals:1")
	}
	stage('Run Tests') 
	{
		try 
		{  
		    sh "mvn test"
			sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD -e $EMAIL_ID"
		    docker.build("belalansari/abctravals:1").push()
			
		} catch (error)
		{
			println("Error in test stage" + error)
		} 
	}
	stage('deploy')
	{
		sh '/home/ubuntu/kubernetes/platforms/linux/amd64/kubectl get podes'
		sh '/home/ubuntu/kubernetes/platforms/linux/amd64/kubectl get nodes'
		sh '/home/ubuntu/kubernetes/platforms/linux/amd64/kubectl apply -f ./deploy1.yaml'
	}
}
