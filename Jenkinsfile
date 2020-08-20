pipeline {
   agent any
   environment 
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        IMAGE = "$PROJECT:$VERSION"
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
                       docker.build('$IMAGE')
                 }
             }
         }
         stage('Push Image'){
         steps{
             script
                {
                   
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(IMAGE).push()
                    }
                }
            }
         }
       stage('Test') {
       agent {
            ecs {
               cloud 'aws-claims'
               launchType 'FARGATE'
               memory 2048
               cpu 1024
               assignPublicIp false
               inheritFrom 'docker'
               label 'sbt'
            }
         }
       }
    }    
}
