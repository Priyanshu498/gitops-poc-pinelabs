pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Detect Environment') {
            steps {
                script {

                    def branch = sh(
                        script: "git rev-parse --abbrev-ref HEAD",
                        returnStdout: true
                    ).trim()

                    echo "Current Branch: ${branch}"

                    if (branch == "dev") {
                        env.DEPLOY_ENV = "dev"
                    }
                    else if (branch == "qa") {
                        env.DEPLOY_ENV = "qa"
                    }
                    else if (branch == "main") {
                        env.DEPLOY_ENV = "prod"
                    }

                    echo "Deploy ENV: ${env.DEPLOY_ENV}"
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
