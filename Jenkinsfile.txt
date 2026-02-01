pipeline {
    agent any

    stages {
        stage('Build & Test (main)') {
            when {
                branch 'main'
            }
            steps {
                sh 'mvn test'
            }
        }

        stage('Test Only (feature)') {
            when {
                expression { env.BRANCH_NAME.startsWith('feature') }
            }
            steps {
                sh 'mvn test'
            }
        }

        stage('Release Checks') {
            when {
                expression { env.BRANCH_NAME.startsWith('release') }
            }
            steps {
                sh 'mvn test'
                echo 'Security scan placeholder'
            }
        }
    }
}
