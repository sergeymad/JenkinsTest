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
                   ssh -i /var/lib/jenkins/.ssh/id_rsa root@206.81.18.96 "cd /var/www/dev/testjenkins/ && git checkout -f ${GIT_BRANCH} && git pull"
                '''
                echo "----------check git branch---------"

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