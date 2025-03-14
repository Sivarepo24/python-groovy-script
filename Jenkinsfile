pipeline {
    agent any

    environment {
        VIRTUAL_ENV = 'venv'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sivarepo24/python-groovy-script.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Test') {
            steps {
                sh '''
                . venv/bin/activate
                pytest test_app.py
                '''
            }
        }
    }
    
    post {
    always {
        mail to: 'sivadevops24@gmail.com',
             subject: "Pipeline status: ${currentBuild.result}",
             body: "Build status: ${currentBuild.result}\nBuild number: ${currentBuild.number}\nCheck console output: ${env.BUILD_URL}"
        cleanWs()
        }
    }
}
