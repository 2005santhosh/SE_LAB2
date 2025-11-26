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
                        venv\\Scripts\\activate  # Correct way to activate virtualenv on Windows
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
                        venv\\Scripts\\activate  # Activate virtual environment
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
