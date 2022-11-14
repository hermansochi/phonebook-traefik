pipeline {
    agent any
    options {
        timestamps()
    }
    stages {
        stage ('Prod') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([
                    string(credentialsId: 'PRODUCTION_HOST', variable: 'HOST'),
                    string(credentialsId: 'PRODUCTION_PORT', variable: 'PORT'),
                ]) {
                    sshagent (credentials: ['PRODUCTION_AUTH']) {
                        sh 'make deploy'
                    }
                }
            }
        }
    }
    post {
        failure {
            withCredentials([string(credentialsId: 'telegramToken', variable: 'TOKEN'), string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')]) {
                sh  ("""
                   curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC  *Branch*: ${env.GIT_BRANCH} *Build* : `not OK`'
                """)
            }
        }
    }
}