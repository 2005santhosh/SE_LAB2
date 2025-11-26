pipeline {
    agent any     

    environment {
        PYTHON_VERSION = "python3"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'rm -rf *'
                    sh """
                        $PYTHON_VERSION -m venv venv
                        source venv/bin/activate
                        pip install -r requirements.txt
                    """
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh """
                        source venv/bin/activate
                        pytest tests/
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up'
            sh 'deactivate'
        }
        success {
            echo 'Build and tests passed successfully!'
        }
        failure {
            echo 'Build or tests failed. Please check the logs.'
        }
    }
}
