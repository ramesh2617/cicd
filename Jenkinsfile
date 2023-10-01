pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
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
                          withDockerRegistry(credentialsId: 'f3a61d0f-85f2-4f8c-95b0-8d4f75941e90', toolName: 'Docker') {
                            sh "docker build ."
                            sh "docker tag my-apache2 mahiramesh2617/mynginx:latest"
                            sh "docker push mahiramesh2617/mynginx:latest "
                        }
                    } 
            }
        }
        
    }
}
