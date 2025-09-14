pipeline {
    agent any

    tools {
        // Make sure Jenkins has a JDK named 'JDK 21' configured
        jdk 'JDK 21'
        maven 'Maven 3' // Ensure you have a Maven installation named 'Maven 3'
    }

    environment {
        // Optional: Email recipient
        EMAIL_RECIPIENT = 'your_email@example.com'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub using your credentials ID
                git credentialsId: 'github-token', url: 'https://github.com/SuryaVelmurugesan/simple_java_ci.git'
            }
        }

        stage('Build') {
            steps {
                // Build the Java project using Maven
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the generated JAR files
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            // Optional: Send email notification on success
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Good news! The build succeeded.\n\nCheck the Jenkins console output: ${env.BUILD_URL}"
        }
        failure {
            echo 'Build failed!'
            // Optional: Send email notification on failure
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Oops! The build failed.\n\nCheck the Jenkins console output: ${env.BUILD_URL}"
        }
    }
}
