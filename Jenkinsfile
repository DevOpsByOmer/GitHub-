pipeline {
    agent any

    tools {
        nodejs "NODE" 
        jdk "JDK"
        maven "MVN"

    }

    stages {
        stage('Fetching the COde') {
            steps {
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
            environment{
                sonarHome = tool 'sonar'                
            }
           steps {
                withSonarQubeEnv('sonarqube') {
               sh '''${sonarHome}/bin/sonar-scanner -Dsonar.projectKey=reactapp \
                    -Dsonar.projectName=reactapp \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/'''
              }
        }
        }
    }

    
  
      
