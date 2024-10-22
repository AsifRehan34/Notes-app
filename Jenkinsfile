pipeline {
    agent any
    
    stages
    {
        stage("Clone code")
        {
             steps
            {
             echo "cloning from github" 
             git url: "https://github.com/AsifRehan34/Notes-app.git" , branch: "main"
            }

        }
        stage("Build code")
        {
             steps
            {
              echo "Building image"
              sh "docker build -t my-notes-app ."
            }
            
        }
        stage("push to Docker Hub")
        {
             steps
            {
               echo "Pushing image to docker Hub" 
               withCredentials([usernamePassword(credentialsId:"Docker-Hub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
               sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
               sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
               sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
               }
              
            }
            
        }
        stage("Deployment")
        {
             steps
            {
              echo "Deploying container to AWS"  
              sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
