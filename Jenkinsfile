pipeline {
    agent any
    stages{
        stage("clone"){
            steps{
                 echo "cloning code from repoistry "
            git url: "https://github.com/mohd-khan09/django-notes-app.git", branch: "main"
            }
             
        }
        stage("build  "){
            steps{
                 echo "build docker image"
                 sh "docker build -t my-note-app ."
            }
           
        }
        stage("Push to docker hub "){
            steps{
                echo "Pushing to docker hub "
                 withCredentials([usernamePassword(credentialsId: "dockerhub_credentials", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
                    sh "docker tag my-note-app ${env.DOCKER_USERNAME}/my-note-app:latest"
                    sh "docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}"
                    sh "docker push ${env.DOCKER_USERNAME}/my-note-app:latest"
                 } 
          
            }
            
        }
        stage("deploy"){
            steps{
                 echo "deploying code to public "
                 sh "docker compose down && docker-compose up -d "
            }
            
        }
    }
}
