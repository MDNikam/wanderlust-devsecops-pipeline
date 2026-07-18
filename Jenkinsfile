pipeline {
    agent any

    environment {
        BACKEND_DIR = 'backend'
        FRONTEND_DIR = 'frontend'
    }

    stages {

        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Verify Workspace') {
            steps {
                sh '''
                echo "Current Directory:"
                pwd

                echo "Repository Contents:"
                ls -la
                '''
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh '''
                    npm install
                    '''
                }
            }
        }

        stage('Verify Backend Packages') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh '''
                    npm list --depth=0
                    '''
                }
            }
        }

        stage('Backend Formatting Check') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh '''
                    npm run check
                    '''
                }
            }
        }

        stage('Backend Unit Tests') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh '''
                    npm run test:ci
                    '''
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh '''
                    npm install
                    '''
                }
            }
        }

        stage('Frontend Build') {
            steps {
                dir("${FRONTEND_DIR}") {
                    sh '''
                    npm run build
                    '''
                }
            }
        }
    }

    post {

        success {
            echo '================================='
            echo 'Build Completed Successfully'
            echo '================================='
        }

        failure {
            echo '================================='
            echo 'Build Failed'
            echo '================================='
        }

        always {
            cleanWs()
        }
    }
}