pipeline {
   agent none
 
    stages {
         stage('Deploy to ECS') {
         agent {
            ecs {
               cloud 'Jenkins-ECS'
               launchType 'FARGATE'
               memory 1024
               cpu 512
               assignPublicIp true
               image '531359658382.dkr.ecr.ap-south-1.amazonaws.com/nodeapp:9'
	       inheritFrom 'ECS-label'
               label 'ECS-label'
                }
            }
		 steps{
			 sh 'java -version'
      }
          }
    }    
}
