pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'echo "Build Complete!"'
            }
        }
        stage('Initial Check') {
            steps {
                echo 'Performing initial checks...'
                sh 'echo "Initial Checks Passed!"'
            }
        }
        stage('Parallel Execution') {
            parallel {
                stage('Copy to Server A') {
                    steps {
                        echo 'Copying files to Server A...'
                        sh 'echo "Files copied to Server A."'
                    }
                }
                stage('Copy to Server B') {
                    steps {
                        echo 'Copying files to Server B...'
                        sh 'echo "Files copied to Server B."'
                    }
                }
            }
        }
    }
    post {
    success {
        emailext to: 'anastas.acevski@outlook.com',
                 subject: 'Jenkins Pipeline Success',
                 body: '''<p>The pipeline executed successfully.</p>''',
                 mimeType: 'text/html'
    }
    failure {
        emailext to: 'anastas.acevski@outlook.com',
                 subject: 'Jenkins Pipeline Failure',
                 body: '''<p>The pipeline has failed. Please check the logs.</p>''',
                 mimeType: 'text/html'
    }
}