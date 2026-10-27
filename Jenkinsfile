pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile hello.py'
            }
        }

        stage('Test') {
            steps {
                sh 'python test.py'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
