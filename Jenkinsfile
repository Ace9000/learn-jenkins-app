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
        always {
            script {
                echo "Sending notification email"
            }
            emailext (
                subject: 'Build Status: ${currentBuild.currentResult}',
                body: """
                    <p>Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) has finished with status: ${currentBuild.currentResult}</p>
                    <p>Check the console output for details: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                to: 'anastas.acevski@outlook.com'
            )
        }
    }
}