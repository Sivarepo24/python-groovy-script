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
            emailext(
                subject: "Pipeline status: ${currentBuild.result}",
                body: '''<html>
                           <body>
                           <p>Build Status: ${currentBuild.result}</p>
                           <p>Build Number: ${currentBuild.number}</p>
                           <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p>
                           </body>
                        </html>''',
                to: 'sivadevops24@gmail.com',
                from: 'sivadevops24@example.com',
                replyTo: 'sivadevops24@example.com',
                mimeType: 'text/html'
            )
            cleanWs()
        }
    }
}
