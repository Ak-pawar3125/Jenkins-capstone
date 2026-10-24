
pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['Build', 'Lint', 'Test', 'Package', 'Production'],
            description: 'Select the pipeline task or deployment environment'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Quality') {
            parallel {
                stage('Build') {
                    steps {
                        bat 'echo Building'
                    }
                }

                stage('Lint') {
                    steps {
                        bat 'echo Linting'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                bat 'echo Testing'
            }
        }

        stage('Package') {
            steps {
                bat 'echo Packaging'
            }
        }

        stage('Approve') {
            when {
                expression {
                    params.ENVIRONMENT == 'Production'
                }
            }
            steps {
                input message: 'Deploy to production?'
            }
        }

        stage('Deploy') {
            when {
                expression {
                    params.ENVIRONMENT == 'Production'
                }
            }
            steps {
                bat 'echo Deploying to Production'
            }
        }
    }

    post {
        success {
            echo 'CI pipeline completed successfully'
        }
        failure {
            echo 'CI pipeline failed'
        }
    }
}
