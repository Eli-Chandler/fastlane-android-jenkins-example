pipeline {
    agent { label 'fastlane-android' }

    environment {
        ARTIFACTORY_API_KEY = credentials('artifactory-api-key')
        ARTIFACTORY_ENDPOINT = 'https://artifactory.infra-go.net/artifactory/'
        ARTIFACTORY_REPO = 'minigame-android'
        ARTIFACTORY_REPO_PATH = 'v1'
    }

    stages {
        stage('Install bundle') {
            steps {
                bat 'bundle install'
            }
        }
        stage('Create Keystore file') {
            steps {
                withCredentials([file(credentialsId: 'temp-android-keystore-file', variable: 'KEYSTORE')]) {
                    bat "echo ${KEYSTORE} > jenkins.keystore"
                }
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
