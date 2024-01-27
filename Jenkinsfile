def COLOR_MAP = [
    SUCCESS: 'good', 
    FAILURE: 'danger',
]

pipeline {
    agent any

    environment {
        SONAR_URL = "http://192.168.33.10:9000"
        JAVA_HOME = tool('JDK')  // Set the correct tool name for JDK
    }

    tools {
        nodejs "NODE" 
        jdk "JDK"
        maven "MVN"
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Fetching the Code') {
            steps {
                sh "git clone https://github.com/DevOpsByOmer/GitHub-.git"
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
                withSonarQubeEnv('sonarqube') {
                    sh '''/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar/bin/sonar-scanner -X -Dsonar.projectKey=reactapp \
                        -Dsonar.projectName=reactapp \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=/var/lib/jenkins/workspace/React_project/GitHub-/src/'''
                }
            }
        }
    }

    post {
        always {
            echo 'Slack Notification.'
            slackSend channel: '#jenkinscice',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n"
        }
    }
}
