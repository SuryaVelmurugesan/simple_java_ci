pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/<username>/SampleJavaApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            // Optional: send email or Slack notification
        }
        failure {
            echo 'Build failed!'
            // Optional: send email or Slack notification
        }
    }
}
