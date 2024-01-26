pipeline {
    agent any

    environment {
       node = "NODE"
        SONAR_URL = "http://192.168.33.10:9000"
    }

    tools {
        nodejs "NODE" 
        jdk "JDK"
        maven "MVN"

    }

    stages {
        stage('CODE CHECKOUT') {
            steps {
                script{
                    sh "git clone https://github.com/DevOpsByOmer/GitHub-.git"
                }
            }
        }
         
        stage('Install Dependencies') {
            steps {
                script {
                  
                    sh 'cd GitHub- && npm install'
                }
            }
            
        }

        stage('Build') {
            steps {
                script {
                    sh 'cd GitHub- && npm run build'
                }
            }
        }
        stage('Sonar Code Analysis') {
            steps {
                script {
                     withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')])
                  
                    sh 'mvn sonar:sonar -Dsonar.url=${SONAR_URL} -Dsonar.login=$SONAR_AUTH_TOKEN'
                }
            }
        }
        }

    }


    
      
