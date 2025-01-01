pipeline{
    agent any
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
                git url:"https://github.com/varikuppalahemanth/django-notes-app.git",branch:"main"
            
            }
        }
        stage("Code Build"){
            steps{
                sh "docker build -t my-notes-app ."
            
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerKey",usernameVariable:"dockerHubuser",passwordVariable:"dockerHubpass")]){
                    sh "docker tag my-notes-app ${env.dockerHubuser}/my-notes-app:latest"
                    sh "docker login -u ${env.dockerHubuser} -p ${env.dockerHubpass}"
                    sh "docker push ${env.dockerHubuser}/my-notes-app:latest"
                }
                
                
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down $$ docker-compose up -d"
                
            }
        }
        
    }
}
