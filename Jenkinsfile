pipeline {
    agent any

    tools {
        jdk 'JDK 21'
        maven 'Maven 3'
    }

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
                 subject: "Jenkins Build SUCCESS: ${currentBuild.fullDisplayName}",
                 body: "Good news! The build succeeded.\n\nCheck it here: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'suryavelmurugesan@gmail.com',
                 subject: "Jenkins Build FAILURE: ${currentBuild.fullDisplayName}",
                 body: "Oops! The build failed.\n\nCheck the details: ${env.BUILD_URL}"
        }
    }
}
