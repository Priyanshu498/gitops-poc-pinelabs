pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Priyanshu498/gitops-poc-pinelabs.git',
                credentialsId: 'github-priyanshu-poc'
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

                    if (msg.contains("env=dev")) {
                        env.DEPLOY_ENV = "dev"
                    }

                    if (msg.contains("env=qa")) {
                        env.DEPLOY_ENV = "qa"
                    }

                    if (msg.contains("env=prod")) {
                        env.DEPLOY_ENV = "prod"
                    }

                    echo "Detected ENV: ${env.DEPLOY_ENV}"
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
