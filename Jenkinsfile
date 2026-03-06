pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}",
                url: 'https://github.com/Priyanshu498/gitops-poc-pinelabs.git',
                credentialsId: 'github-priyanshu-poc'
            }
        }

        stage('Detect Environment') {
            steps {
                script {

                    if (env.BRANCH_NAME == "dev") {
                        env.DEPLOY_ENV = "dev"
                    }

                    else if (env.BRANCH_NAME == "qa") {
                        env.DEPLOY_ENV = "qa"
                    }

                    else if (env.BRANCH_NAME == "main") {
                        env.DEPLOY_ENV = "prod"
                    }

                    echo "Branch = ${env.BRANCH_NAME}"
                    echo "Deploy Environment = ${env.DEPLOY_ENV}"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {

                    if (env.DEPLOY_ENV == "dev") {
                        sh 'echo Deploying to DEV'
                    }

                    if (env.DEPLOY_ENV == "qa") {
                        sh 'echo Deploying to QA'
                    }

                    if (env.DEPLOY_ENV == "prod") {
                        sh 'echo Deploying to PROD'
                    }

                }
            }
        }

    }
}
