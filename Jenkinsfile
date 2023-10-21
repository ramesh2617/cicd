pipeline {
    agent any
    
    tools {
         maven 'maven3'
    }

    stages {
        stage('Git Checkout') {
            steps {
               git branch: 'main', changelog: false, poll: false, url: 'https://github.com/ramesh2617/SpringBoot-WebApplication.git'
            }
        }
         stage('Code Compile') {
            steps {
                    sh "mvn compile"
            }
        }
        stage('Run Test Cases') {
            steps {
                    sh "mvn test"
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                   script {
                       // This step should not normally be used in your script. Consult the inline help for details.
                       withDockerRegistry(credentialsId: '75f6c593-f2dc-4681-89d9-56156439bd9c', url: 'https://hub.docker.com/') {
                         // some block
                           }
                            sh "docker build ."
                            sh "docker tag my-apache2 mahiramesh2617/myargo mynginx:latest"
                            sh "docker push mahiramesh2617/myargo mynginx:latest "
                        }
                    } 
            }
        }
        
}
