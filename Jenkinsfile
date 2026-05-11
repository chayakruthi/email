pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pulls your code from GitHub
                git branch: 'main', 
                    url: 'https://github.com/chayakruthi/email.git', 
                    credentialsId: 'github-token'
            }
        }

        stage('Verify Content') {
            steps {
                // This lists your files in the log so you can see what's actually there
                sh 'ls -la'
                echo "This is not a Maven project, so we are just verifying files."
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: ${JOB_NAME} [Build #${BUILD_NUMBER}]",
                body: "The files were checked out successfully. View build: ${BUILD_URL}",
                to: "cmchaya37@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "FAILED: ${JOB_NAME} [Build #${BUILD_NUMBER}]",
                body: "Something went wrong. Check the logs: ${BUILD_URL}",
                to: "cmchaya37@gmail.com"
            )
        }
    }
}
