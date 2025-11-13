pipeline {
    agent any

    environment {
        PYTHON = "C:\\Users\\User\\AppData\\Local\\Programs\\Python\\Python313\\python.exe"
        VENV   = "venv"
    }

    stages {

        stage('Setup') {
            steps {
                script {
                    // Create virtual environment
                    bat "\"${PYTHON}\" -m venv ${VENV}"

                    // Install dependencies
                    bat """
                        ${VENV}\\Scripts\\python.exe -m pip install --upgrade pip
                        ${VENV}\\Scripts\\pip.exe install -r requirements.txt
                    """
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    bat """
                        ${VENV}\\Scripts\\flake8.exe app.py
                    """
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    bat """
                        ${VENV}\\Scripts\\pytest.exe
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy stage completed successfully."
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
