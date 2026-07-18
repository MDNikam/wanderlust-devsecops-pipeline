pipeline {
    agent any

    options {
        timestamps()
        ansiColor('xterm')
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Workspace') {
            steps {
                sh '''
                    echo "Current Workspace:"
                    pwd
                    echo ""
                    echo "Repository Contents:"
                    ls -la
                '''
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('backend') {
                    sh '''
                        npm ci
                    '''
                }
            }
        }

        stage('Verify Backend') {
            steps {
                dir('backend') {
                    sh '''
                        npm list --depth=0
                    '''
                }
            }
        }

        stage('Prettier Check') {
            steps {
                dir('backend') {
                    sh '''
                        npm run check
                    '''
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('frontend') {
                    sh '''
                        npm ci
                    '''
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    sh '''
                        npm run build
                    '''
                }
            }
        }

    }

    post {
        always {
            echo "Pipeline Finished"
        }

        success {
            echo "Build Successful"
        }

        failure {
            echo "Build Failed"
        }
    }
}
