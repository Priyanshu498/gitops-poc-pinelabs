pipeline {
agent any

stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Read Commit Message') {
        steps {
            script {

                def msg = sh(
                    script: "git log -1 --pretty=%B",
                    returnStdout: true
                ).trim()

                echo "Commit message: ${msg}"

                // default environment
                env.DEPLOY_ENV = "dev"

                if (msg.contains("env=dev")) {
                    env.DEPLOY_ENV = "dev"
                }
                else if (msg.contains("env=qa")) {
                    env.DEPLOY_ENV = "qa"
                }
                else if (msg.contains("env=prod")) {
                    env.DEPLOY_ENV = "prod"
                }
            }
        }
    }

    stage('Branch Info') {
        steps {
            script {
                echo "Branch = ${env.GIT_BRANCH}"
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
