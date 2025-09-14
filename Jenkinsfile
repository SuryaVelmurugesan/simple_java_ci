pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'suryavelmurugesan@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/SuryaVelmurugesan/simple_java_ci.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: false
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build succeeded!\n\nCheck console: ${env.BUILD_URL}"
        }
        failure {
            echo 'Build failed!'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed!\n\nCheck console: ${env.BUILD_URL}"
        }
    }
}
