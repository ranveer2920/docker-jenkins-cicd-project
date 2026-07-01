pipeline {
    agent any

    options {
        // Automatically discards old builds to preserve disk space
        buildDiscarder logRotator(numToKeepStr: '10') 
        // Prevents parallel execution of the same branch
        disableConcurrentBuilds() 
    }

    stages {
        stage('Checkout') {
            steps {
                // Safely checks out the exact branch and revision that triggered the build
                checkout scm 
            }
        }

        stage('Build & Test') {
            steps {
                echo "Running standard verification tasks on branch: ${env.BRANCH_NAME}"
                // Add your project-specific compilation or testing scripts here
                // Example: sh 'npm install && npm test'
            }
        }

        stage('Deploy to Staging') {
            // This stage only executes if the active branch is 'develop'
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying artifact to the Staging Environment..."
                // Example: sh './deploy_staging.sh'
            }
        }

        stage('Deploy to Production') {
            // This stage only executes if the active branch is 'main' or 'master'
            when {
                branch 'main'
            }
            steps {
                echo "Deploying artifact to the Production Environment..."
                // Example: sh './deploy_prod.sh'
            }
        }
    }

    post {
        always {
            echo "Pipeline cleanup or notification logic goes here."
        }
        success {
            echo "Build finished successfully!"
        }
        failure {
            echo "Build failed. Investigate the console output."
        }
    }
}
