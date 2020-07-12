pipeline {
    agent none

    stages {
        stage('StopRemove') {
            agent { 
                label 'devops_docker_2'
            }
            
            steps {
                sh 'ls -l'
                sh 'docker container stop dptwo'
                sh 'docker container rm dptwo'
                sh 'docker image rmi akhil5001/devops_docker_2:latest'
            }
        }
        stage('Build') {
            agent { 
                label 'devops_docker_2'
            }
            
            
            steps {
                sh 'docker build -t  akhil5001/devops_docker_2 .'
                sh 'docker container run -d --name dptwo -p 80:80 akhil5001/devops_docker_2:latest'
                
            }
        }
        stage('Push') {
            when {
                branch 'finance'  //only run these steps on the development branch
            }
            agent { 
                label 'devops_docker_2'
            }
            
            steps {
                sh 'docker push akhil5001/devops_docker_2:latest'
                
            }
        }
        stage('Deploy') {
            agent { 
                label 'labeldockerserver'
            }
            
            steps {
                sh 'docker container stop dptwo'
                sh 'docker container rm dptwo'
                sh 'docker image rmi akhil5001/devops_docker_2:latest'
                sh 'docker container run -d --name dptwo -p 80:80 akhil5001/devops_docker_2:latest'
                
            }
        }
    }
}
