pipeline {
    agent any

    stages {

        stage('Detect Environment') {
            steps {
                script {

                    def branch = env.GIT_BRANCH
                    echo "Git Branch: ${branch}"

                    if (branch.contains("dev")) {
                        env.DEPLOY_ENV = "dev"
                    }
                    else if (branch.contains("qa")) {
                        env.DEPLOY_ENV = "qa"
                    }
                    else if (branch.contains("main")) {
                        env.DEPLOY_ENV = "prod"
                    }

                    echo "Deploy Environment: ${env.DEPLOY_ENV}"
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
