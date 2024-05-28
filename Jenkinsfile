pipeline {
    agent {
        node {
            label "win11-test"
        }
    }
    
    environment {
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Auto upload') {
            steps {
                script {
                    bat 'copy D:\Jenkins\remoting\update_all_files_pro630.py ${WORKSPACE}'
                    bat 'python ${WORKSPACE}\update_all_files_pro630.py'
                }
            }
        }

        } 
    }

