pipeline {
        docker {
            image 'elichandler/docker-android-fastlane-bash-entrypoint:latest'
        }

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

        stage('Run fastlane') {
            steps {
                // Set environment variables
                withCredentials([file(credentialsId: 'temp-android-keystore-file', variable: 'KEYSTORE')]) {
                    withEnv(["ARTIFACTORY_API_KEY=${ARTIFACTORY_API_KEY}",
                             "ARTIFACTORY_ENDPOINT=${ARTIFACTORY_ENDPOINT}",
                             "ARTIFACTORY_REPO=${ARTIFACTORY_REPO}",
                             "ARTIFACTORY_REPO_PATH=${ARTIFACTORY_REPO_PATH}",
                             "KEYSTORE_PATH=${KEYSTORE}"]) {
                        bat 'bundle exec fastlane deployInFirebase'

                    }
                }
            }
        }
    }
}
