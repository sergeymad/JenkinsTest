pipeline {
    agent any
    parameters {
        choice(
            choices: ['CheckoutSCM','dev'],
            name: 'namespace'
        )
    }

    stages {
        stage("Deploy") {
            when {
                expression { params.namespace == 'dev' }
            }
            steps {
                echo "----------Start build---------"
                sh '''
                   "git checkout -f ${GIT_BRANCH} && git pull"
                '''
                echo "----------check git branch---------"
                  sh '''
                    "npm i && npm run build && npm run start"
                     '''
                echo "----------End build---------"
            }
        }
        stage('Checkout SCM') {
            when {
                expression { params.namespace == 'CheckoutSCM' }
            }
            steps {
                echo 'CheckoutSCM'
            }
        }
    }
}