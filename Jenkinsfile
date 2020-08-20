pipeline {
   agent any
   environment 
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        DOCKER_IMAGE = "$PROJECT:$VERSION"
        ECRURL = 'https://531359658382.dkr.ecr.ap-south-1.amazonaws.com/node_app'
        ECRCRED = 'ecr:ap-south-1:ECR_Creds'
    }   
    stages {
      stage('GetSCM') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/ChetanKumar07/Docker-ECR.git'
         }
         }
         stage('Image Build'){
             steps{
                 script{
                       docker.build('$DOCKER_IMAGE')
                 }
             }
         }
         stage('Push Image'){
         steps{
             script
                {
                   
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
         }
       stage('Deploy to ECS') {
       agent {
            ecs {
               cloud 'Jenkins-ECS'
               launchType 'FARGATE'
               memory 2048
               cpu 1024
               assignPublicIp false
               image '531359658382.dkr.ecr.ap-south-1.amazonaws.com/node_app:28'
               label 'ECS-label'
            }
         }
       }
    }    
}
