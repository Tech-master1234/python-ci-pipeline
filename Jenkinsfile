pipeline {
    agent {
        docker {
            image 'python:3.10'   // Official Python image with pip preinstalled
        }
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                python -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest test_app.py --junitxml=test-results.xml
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                . venv/bin/activate
                python app.py
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results.xml'
        }
    }
}
