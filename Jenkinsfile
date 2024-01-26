pipeline {
    agent any

    environment {
       node = 'NODE'
    }

    tools {
        nodejs "NODE" 
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

    }
}

    
      
