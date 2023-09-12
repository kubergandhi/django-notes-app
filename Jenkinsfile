pipeline {
    agent any 
    
    stages{ 
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                sh "docker push ${dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container!!"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
