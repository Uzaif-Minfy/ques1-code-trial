pipeline {
    agent any

    stages {
        stage('Prepare') {
            steps {
                echo 'Creating deploy.conf and deploy.sh...'
                sh 'echo "config data" > deploy.conf'
                sh 'echo "echo Deploying..." > deploy.sh'
                sh 'chmod +x deploy.sh'
            }
        }

        stage('Check and Deploy') {
            steps {
                script {
                    // Your exact one-liner condition
                    if (sh(script: 'test -f deploy.conf', returnStatus: true) == 0) {
                        sh 'deploy.sh'
                    } else {
                        error 'deploy.conf not found — failing build.'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -f deploy.conf deploy.sh'
        }
    }
}
