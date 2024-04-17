pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Harsh2532/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
         stage("Test Case Verification"){
            steps {
                echo "tested the code"
            }
        }
        stage("Filteration"){
            steps {
                echo "Filtered the code"
            }
        }
        
        stage("Pushed to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag my-note-app ${env.dockerhubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/my-note-app:latest"
                }
            }
        }
       stage("Deploy") {
        steps {
            echo "Deploying the container"
            sh 'echo "PATH: $PATH"' // Print PATH environment variable
            sh 'which docker-compose' // Print the location of docker-compose binary
            sh 'docker-compose down' // Execute docker-compose down
            sh 'docker-compose up -d' // Execute docker-compose up
        }
}
