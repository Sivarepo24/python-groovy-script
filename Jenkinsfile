pipeline{
    agent any

    environment {
        VIRTUAL_ENV = 'venv'
    }

    stages{
        stage('clone Repository'){
            steps{
                git branch:'main', url: 'https://github.com/Sivarepo24/python-groovy-script.git'
                }
            }
        
        stage('Build'){
            steps{
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        
        stage('Run Test'){
            steps{
                sh '''
                . venv/bin/activate
                pytest test_app.py
                '''
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}