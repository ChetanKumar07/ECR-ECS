pipeline {
   agent none
   environment 
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        DOCKER_IMAGE = "$PROJECT:$VERSION"
        ECRURL = 'https://531359658382.dkr.ecr.ap-south-1.amazonaws.com/node_app'
        ECRCRED = 'ecr:ap-south-1:ECR_Creds'
    }   
    stages {
         stage('Deploy to ECS') {
		 steps {
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
          }
		}
    }    
}
