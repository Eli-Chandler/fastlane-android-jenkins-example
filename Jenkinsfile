pipeline {
    agent { label 'fastlane' }

    environment {
        ARTIFACTORY_API_KEY = credentials('artifactory-api-key')
        ARTIFACTORY_ENDPOINT = 'https://artifactory.infra-go.net/artifactory/
        ARTIFACTORY_REPO = 'minigame-android'
        ARTIFACTORY_REPO_PATH = 'v1'
    }

    stages {
        stage('Install bundle') {
            steps {
                bat 'bundle install'
            }
        }
        stage('Run fastlane') {
            steps {
                // Set environment variables
                withEnv(["ARTIFACTORY_API_KEY=${ARTIFACTORY_API_KEY}",
                         "ARTIFACTORY_ENDPOINT=${ARTIFACTORY_ENDPOINT}",
                         "ARTIFACTORY_REPO=${ARTIFACTORY_REPO}",
                         "ARTIFACTORY_REPO_PATH=${ARTIFACTORY_REPO_PATH}"]) {
                    bat 'bundle exec fastlane deployInFirebase'
                }
            }
        }
    }
}
