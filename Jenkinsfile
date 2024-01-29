pipeline {
    agent any

    environment {
       node = 'NODE'
    }

    tools {
        nodejs "NODE" 
    }

    stages {
         stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
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
             post {
        always {
            echo 'Slack Notification.'
            slackSend channel: '#jenkinscicd',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n",
                botUser: false,
                tokenCredentialId: 'slacktoken',
                notifyCommitters: false
        }
    }
        }

    }
}

    
      
