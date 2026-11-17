
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Fetching code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Python Application'
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Python Application'
                sh 'python3 test_app.py'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running Application'
                sh 'python3 app.py'
            }
        }
    }

    post {

        success {
            emailext(
                to: 'mohityadav10137@gmail.com',
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello Student,

Your Jenkins Pipeline executed successfully.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: SUCCESS

Build URL: ${env.BUILD_URL}

Thank You!
"""
            )
        }

        failure {
            emailext(
                to: 'student@gmail.com',
                subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello Student,

Your Jenkins Pipeline has failed.

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: FAILURE

Please check Jenkins Console Output.

Build URL: ${env.BUILD_URL}
"""
            )
        }
    }
}
