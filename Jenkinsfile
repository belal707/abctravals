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
	stage('Test Kubectl command')
	{
		sh "kubectl get nodes"
	}
	stage('Run Tests') 
	{
		try 
		{  
		    sh "mvn test"
			sh "docker login -u belalansari -p zamila1234 -e belalansari23@gmail.com"
		    docker.build("belalansari/abctravals:10").push()
			
		} catch (error)
		{

		} 
	}	
}
