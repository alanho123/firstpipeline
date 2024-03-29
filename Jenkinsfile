pipeline {
    agent { docker 'maven:3.3.3' }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
            post {
                always {
                    echo 'This will always run'
                }
                success {
                    echo 'This will run only if successful'
                    slackSend channel: '#website',
                                color: 'good',
                                message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
                }
                failure {
                    echo 'This will run only if failed'
                }
                unstable {
                    echo 'This will run only if the run was marked as unstable'
                }
                changed {
                    echo 'This will run only if the state of the Pipeline has changed'
                    echo 'For example, if the Pipeline was previously failing but is now successful'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing'
            }
        }

        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
}
