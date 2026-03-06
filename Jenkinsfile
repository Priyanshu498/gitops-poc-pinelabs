pipeline {
    agent any

    parameters {
        choice(
            name: 'ENV',
            choices: ['dev', 'qa', 'prod'],
            description: 'Select environment'
        )
    }

    environment {
        ENV = "${params.ENV ?: 'dev'}"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Priyanshu498/gitops-poc-pinelabs.git',
                credentialsId: 'github-priyanshu-poc'
            }
        }

        stage('Print Event Info') {
            steps {
                echo "Branch: ${env.GIT_BRANCH}"
                echo "Environment: ${env.ENV}"
                echo "Commit: ${env.GIT_COMMIT}"
            }
        }

        stage('Deploy') {
            steps {
                script {

                    if (env.ENV == 'dev') {
                        sh 'echo Deploying to DEV'
                    }

                    if (env.ENV == 'qa') {
                        sh 'echo Deploying to QA'
                    }

                    if (env.ENV == 'prod') {
                        sh 'echo Deploying to PROD'
                    }

                }
            }
        }

    }
}
