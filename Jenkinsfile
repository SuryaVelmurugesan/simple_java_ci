pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SuryaVelmurugesan/simple_java_ci.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }

    post {
        success {
            mail to: 'suryavelmurugesan@gmail.com',
                 subject: "✅ Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The Jenkins build succeeded.\nCheck details here: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'suryavelmurugesan@gmail.com',
                 subject: "❌ Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The Jenkins build failed.\nCheck details here: ${env.BUILD_URL}"
        }
    }
}
