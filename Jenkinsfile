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
                url: 'https://github.com/org/gitops-poc.git'
            }
        }

        stage('Print Event Info') {
            steps {
                echo "Branch: ${env.GIT_BRANCH}"
                echo "Environment: ${params.ENV}"
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (params.ENV == 'dev') {
                        sh './deploy-dev.sh'
                    }

                    if (params.ENV == 'qa') {
                        sh './deploy-qa.sh'
                    }

                    if (params.ENV == 'prod') {
                        sh './deploy-prod.sh'
                    }
                }
            }
        }
    }
}
