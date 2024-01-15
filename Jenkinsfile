pipeline {
    agent { label 'fastlane' }
    stages {
        stage('Install bundle') {
            steps {
                bat 'bundle install'
            }
        }
        stage('Run fastlane') {
            steps {
                bat 'bundle exec fastlane deployInFirebase'
            }
        }
    }
}
