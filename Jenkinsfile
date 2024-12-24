pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out the repository..."
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Building the Project..."
                echo "Build process simulated."
            }
        }
        stage('Parallel File Copy') {
            steps {
                script {
                    echo "Starting Parallel File Copy..."
                    parallel (
                        "Copy to Location 1": {
                            bat "echo Copying files to Location 1..."
                        },
                        "Copy to Location 2": {
                            bat "echo Copying files to Location 2..."
                        }
                    )
                }
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: """<p style="color:green;">✅ Build <b>#${env.BUILD_NUMBER}</b> succeeded!</p>
                         <p>View logs: <a href='${env.BUILD_URL}'>Build Logs</a></p>""",
                to: "anastas.acevski@outlook.com",
                mimeType: 'text/html'
            )

            script {
                build job: 'SystemStatusReport', wait: false
            }
        }
        
        failure {
            emailext(
                subject: "FAILURE: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                body: """<p style="color:red;">❌ Build <b>#${env.BUILD_NUMBER}</b> failed!</p>
                         <p>View logs: <a href='${env.BUILD_URL}'>Build Logs</a></p>""",
                to: "anastas.acevski@outlook.com",
                mimeType: 'text/html'
            )
        }
    }
}

