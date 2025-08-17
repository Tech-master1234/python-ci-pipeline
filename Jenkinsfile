pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-username/your-repo.git'
            }
        }

    stage('Install Dependencies') {
        steps {
            sh '''
            python3 -m venv venv
            . venv/bin/activate
            python3 -m pip install --upgrade pip
            python3 -m pip install -r requirements.txt
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
        success {
            echo '✅ Build & tests passed!'
        }
        failure {
            echo '❌ Build failed. Check logs!'
        }
    }
}
