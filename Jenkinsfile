pipeline {
    agent { docker { image 'python:3.10.1-alpine' } }

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('build') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'python --version'
            }
        }

        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy - Production') {
            steps {
                sh 'python --version'
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            // mail to: 'xiaoningli@data.ai',
            //  subject: "Success Pipeline: ${currentBuild.fullDisplayName}",
            //  body: "It finished successfully ${env.BUILD_URL}"
        }
        failure {
            echo 'This will run only if failed'
            // mail to: 'xiaoningli@data.ai',
            //  subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            ///  body: "Something is wrong with ${env.BUILD_URL}"
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