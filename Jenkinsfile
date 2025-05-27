pipeline {
    agent any

    stages {
        stage('Prepare') {
            steps {
                echo 'Creating dummy deploy.conf file...'
                sh 'echo "config data" > deploy.conf'
            }
        }

        stage('Check File and Deploy') {
            steps {
                script {
                    if (sh(script: 'test -f deploy.conf', returnStatus: true) == 0) {
                        echo 'File exists, running deploy script...'
                        sh 'echo "Deploying..."'
                    } else {
                        echo 'deploy.conf not found. Skipping deployment.'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -f deploy.conf'
        }
    }
}
