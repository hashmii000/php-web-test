
pipeline {
    agent any

    stages {

        stage('Check PHP Version') {
            steps {
                bat 'php -v'
            }
        }

        stage('Validate PHP Syntax') {
            steps {
                bat 'php -l index.php'
            }
        }

        stage('Build Artifact') {
            steps {
                bat 'powershell Compress-Archive -Path * -DestinationPath build.zip -Force'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }

    }
}
