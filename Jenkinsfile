pipeline {
    agent any

    environment {
        // Define environment variables if needed
        NODE_VERSION = '14' // Specify Node.js version
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your version control system
                git 'git@github.com:skthesujan/devops_initial_learning.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Use Node.js Docker image to install dependencies
                docker.image("node:${NODE_VERSION}")
                      .inside {
                          sh 'npm install'
                      }
            }
        }

        stage('Build') {
            steps {
                // Build your Node.js application
                docker.image("node:${NODE_VERSION}")
                      .inside {
                          sh 'npm run build' // Adjust based on your build command
                      }
            }
        }

        stage('Test') {
            steps {
                // Run tests for your Node.js application
                docker.image("node:${NODE_VERSION}")
                      .inside {
                          sh 'npm test' // Adjust based on your test command
                      }
            }
        }

        stage('Deploy') {
            steps {
                // Example deployment step (adjust as per your deployment strategy)
                sh 'echo Deploying...'
                // Add deployment commands here (e.g., using SSH, Docker, etc.)
            }
        }
    }

    post {
        success {
            echo 'All stages completed successfully!'

            // Example: Send notification on success
            // emailext subject: "Pipeline Success - ${currentBuild.fullDisplayName}",
            //           body: "Pipeline completed successfully.",
            //           recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }

        failure {
            echo 'Pipeline failed :('

            // Example: Send notification on failure
            // emailext subject: "Pipeline Failure - ${currentBuild.fullDisplayName}",
            //           body: "Pipeline failed. Please investigate.",
            //           recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        }
    }
}

