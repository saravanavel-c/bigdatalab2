pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python3 -m py_compile hello.py'
                sh 'python3 hello.py'
                echo 'BUILD COMPLETED'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 test.py'
                echo 'TEST COMPLETED'
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
