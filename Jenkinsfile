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
