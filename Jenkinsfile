pipeline {
    agent any

    environment {
        PYTHON_VERSION = 'python' 
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'rm -rf *'
                    sh '''
                        $PYTHON_VERSION -m venv venv  # Create a virtual environment using Python
                        venv\\Scripts\\activate  # Use Windows path to activate the virtual environment
                        pip install -r requirements.txt  # Install dependencies from requirements.txt
                    '''
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh '''
                        venv\\Scripts\\activate  # Activate the virtual environment
                        pytest tests/  # Run tests (make sure your tests are in a 'tests' folder)
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up'
            sh '''
                if [ -f venv\\Scripts\\activate ]; then
                    deactivate || echo "No virtual environment to deactivate."
                fi
            '''
        }

        success {
            echo 'Build and tests passed successfully!'
        }

        failure {
            echo 'Build or tests failed. Please check the logs.'
        }
    }
}
