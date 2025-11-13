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
                    
                    bat "\"${PYTHON}\" -m venv ${VENV}"

                  
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
            set PYTHONPATH=%WORKSPACE%
            venv\\Scripts\\pytest.exe
            """
        }
    }
}
stage('Coverage') {
    steps {
        script {
            bat """
            set PYTHONPATH=%WORKSPACE%
            venv\\Scripts\\python.exe -m coverage run -m pytest
            venv\\Scripts\\python.exe -m coverage report
            """
        }
    }
}
stage('Security Scan') {
    steps {
        script {
            bat """
            set PYTHONPATH=%WORKSPACE%
            venv\\Scripts\\bandit.exe -r . -f json -o bandit_report.json --exit-zero
            """
        }
        archiveArtifacts artifacts: 'bandit_report.json', allowEmptyArchive: true
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
