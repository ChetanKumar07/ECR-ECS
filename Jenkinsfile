pipeline {
   agent none
 
    stages {
         stage('Deploy to ECS') {
         agent {
            ecs {
               cloud 'Jenkins-ECS'
	       inheritFrom 'ECS-template'
               launchType 'FARGATE'
               memory 1024
               cpu 512
               image '531359658382.dkr.ecr.ap-south-1.amazonaws.com/nodeapp:9'
               label 'ECS-label'
                }
            }
		 steps{
			 sh 'java -version'
      }
          }
    }    
}
