pipeline {
    agent any

    tools {
        jdk 'JDK 21'
        maven 'Maven 3'
    }

    environment {
        EMAIL_RECIPIENT = 'suryavelmurugesan@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], 
                userRemoteConfigs: [[url: 'https://github.com/SuryaVelmurugesan/simple_java_ci.git', 
                                     credentialsId: 'github-token']]])
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
            // Send email if configured properly
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build succeeded!\nDetails: ${env.BUILD_URL}"
        }
        failure {
            echo 'Build failed!'
            mail to: "${EMAIL_RECIPIENT}",
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed!\nCheck: ${env.BUILD_URL}"
        }
    }
}
