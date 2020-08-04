pipeline {
   agent any
   environment 
    {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = 'nodeapp'
        IMAGE = "$PROJECT:$VERSION"
        ECRURL = 'https://531359658382.dkr.ecr.ap-south-1.amazonaws.com/node_app'
        ECRCRED = 'ecr:ap-south-1:uploadtos3'
    }   
    stages {
      stage('GetSCM') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/ChetanKumar07/Docker-ECR.git'
         }
         }
       stage('Create Repo'){
          steps{
             aws ecr create-repository --repository-name node_app1 --region ap-south-1}
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
    }
  
    post
    {
        always
        {
            // make sure that the Docker image is removed
            sh "docker rmi $IMAGE | true"
        }
    }
    
}
