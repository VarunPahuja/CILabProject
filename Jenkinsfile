pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Build & Test (main)') {
            when {
                branch 'main'
            }
            steps {
                bat 'mvn test'
            }
        }

        stage('Test Only (feature)') {
            when {
                expression { env.BRANCH_NAME.startsWith('feature') }
            }
            steps {
                bat 'mvn test'
            }
        }

        stage('Release Checks') {
            when {
                expression { env.BRANCH_NAME.startsWith('release') }
            }
            steps {
                bat 'mvn test'
                echo 'Security scan placeholder'
            }
        }
    }
}
