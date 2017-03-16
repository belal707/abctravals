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
		    docker.build("belalansari/abctravals:10").push()
			
		} catch (error)
		{

		} 
	}	
}
