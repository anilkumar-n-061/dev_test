pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
               git branch: 'staging' , url: https://github.com/anilkumar-n-061/dev_test.git
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js packages...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Unit Tests...'
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Application...'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            when {
                anyOf {
                    branch 'main'
                    branch 'staging'
                }
            }
            steps {
                echo "Deploying to environment based on branch: ${env.BRANCH_NAME}"
                sh './scripts/deploy.sh'
            }
        }
    }

    post {
        success {
            echo '✅ CI/CD pipeline completed successfully!'
        }
        failure {
            echo '❌ CI/CD pipeline failed!'
        }
    }
}
