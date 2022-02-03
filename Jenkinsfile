node{
    environment{
        DOCKERHUB_CREDENTIALS = credentials('raksh8-dockerhub')
    }
    stage("first stage"){
        git 'https://github.com/raksh8/docker-django-new.git'
    }
    stage("build stage"){
        
        sh 'docker build -t mysite_image .'
        sh 'docker tag mysite_image:latest raksh8/django-dockerhub-repo:latest'
        

    }
  // To push the image to docker-hub
    stage("push image to docker hub"){

              withDockerRegistry([credentialsId: "raksh8-dockerhub", url: ""]){
              sh 'docker push raksh8/django-dockerhub-repo:latest'

    }
      
  // To push the image to AWS ECR
      
    stage("push image to ecr"){
        
            script{
                docker.withRegistry(
                    'https://119505610541.dkr.ecr.ap-south-1.amazonaws.com',
                    'ecr:ap-south-1:ecr'){
                        def myImage = docker.build('django-hello-world')
                        myImage.push('latest')
                    }
                
            }
        
        
    }
}
