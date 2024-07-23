pipeline {
    agent any
    
    stages {
        stage('Clone Code') {
            steps {
                echo 'Clone the code from GitHub'
                git branch: 'main', url: 'https://github.com/Rishi5520/django-notes-app.git'
            }
        }
        stage('Build Code') {
            steps {
                echo 'Build your code'
                sh 'docker build -t second-todo-app .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                echo 'Push the code to Docker Hub'
                withCredentials([usernamePassword(credentialsId:"DockerHubID",usernameVariable:"dockerHubUser",passwordVariable:"dockerHubPass")]){
                    sh "docker tag notes-app ${env.dockerHubUser}/notes-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        stage('Deploy to EC2 Instance') {
            steps {
                echo 'Deploy to EC2 Instance'
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
