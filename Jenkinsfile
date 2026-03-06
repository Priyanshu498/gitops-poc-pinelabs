
pipeline {
    agent any

    parameters {
        choice(
            name: 'ENV',
            choices: ['dev', 'qa', 'prod'],
            description: 'Select environment'
        )
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
                echo "Environment: ${params.ENV}"
                echo "Commit: ${env.GIT_COMMIT}"
            }
        }

        stage('Deploy') {
            steps {
                script {

                    if (params.ENV == 'dev') {
                        sh 'echo Deploying to DEV environment'
                        sh './deploy-dev.sh'
                    }

                    if (params.ENV == 'qa') {
                        sh 'echo Deploying to QA environment'
                        sh './deploy-qa.sh'
                    }

                    if (params.ENV == 'prod') {
                        sh 'echo Deploying to PROD environment'
                        sh './deploy-prod.sh'
                    }

                }
            }
        }

    }
}
