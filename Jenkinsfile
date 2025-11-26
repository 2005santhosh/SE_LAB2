pipeline {
    agent any

    environment {
        PYTHON_VERSION = 'python'  // Use 'python' for Windows
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Clean up the workspace
                    sh 'rm -rf *'

                    // Create and activate the virtual environment
                    sh '''
                        python -m venv venv  # Create virtual environment
                        call venv\\Scripts\\activate.bat  # Correct way to activate virtualenv on Windows
                        pip install -r requirements.txt  # Install dependencies
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run the tests
                    sh '''
                        call venv\\Scripts\\activate.bat  # Activate virtual environment
                        pytest tests/  # Run tests (adjust path as needed)
                    '''
                }
            }
        }
    }

    post {
        always {
            // Clean up the environment after build
            echo 'Cleaning up'
            sh '''
                if exist venv\\Scripts\\activate.bat (
                    call venv\\Scripts\\deactivate.bat || echo "No virtual environment to deactivate."
                )
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
