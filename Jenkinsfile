pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checks out the code from your repository.
                checkout scm
            }
        }
        stage('Run Script') {
            steps {
                script {
                    // Jenkins sets BRANCH_NAME for multibranch pipelines.
                    if (env.BRANCH_NAME == 'master') {
                        // For the master branch, run the resizedisk script normally.
                        echo "Running resizedisk.py on master branch..."
                        sh 'python resizedisk.py'
                    } else if (env.BRANCH_NAME?.startsWith("feature")) {
                        // For branches starting with "feature", run the script and then fail intentionally.
                        echo "Running resizedisk.py on a feature branch..."
                        sh 'python resizedisk.py'
                        error("Intentional failure for feature branch")
                    } else {
                        echo "Branch ${env.BRANCH_NAME} does not trigger any specific action."
                    }
                }
            }
        }
    }
}
