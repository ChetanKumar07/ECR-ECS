pipeline {
   agent none
 
    stages {
         stage('Deploy to ECS') {
         agent {
            ecs {
               cloud 'ECR-ECS'
	       inheritFrom 'ECS-template'
	       label 'ECS-label'
               launchType 'EC2'
               memory 1024
               cpu 512
               image '531359658382.dkr.ecr.ap-south-1.amazonaws.com/nodeapp:9'
	       portMappings([[containerPort: 8080, hostPort: 8080, protocol: 'tcp'], [containerPort: 443, hostPort: 443, protocol: 'tcp']])
                }
            }
		 steps{
			 sh 'java -version'
      }
          }
    }    
}
