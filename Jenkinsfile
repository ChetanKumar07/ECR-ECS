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
               assignPublicIp false
               image '531359658382.dkr.ecr.ap-south-1.amazonaws.com/node_app:9'
               label 'ECS-label'
                }
            }
		 Steps{
			 sh 'java -version'
      }
          }
    }    
}
