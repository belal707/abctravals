node 
{
  	checkout scm
  	stage('Package') 
  	{
     	sh 'mvn clean package -DskipTests'
  	}
	stage('Create Docker Image') 
	{
			docker.build("belalansari/abctravals:10")
	}
	stage('Run Tests') 
	{
		try 
		{  
		    sh "mvn test"
			sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD -e $EMAIL_ID"
		    docker.build("belalansari/abctravals:10").push()
			
		} catch (error)
		{
			println("Error in test stage" + error)
		} 
	}
	stage('Test Kubectl command')
	{
		sh '/home/ubuntu/kubernetes/plateform/linux/amd64/kubectl create -f deploy1.yaml'
	}
}
