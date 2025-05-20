pipeline {
    agent any

    tools {
        maven 'M3'
        jdk 'JDK17'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker Build & Push') {
            steps {
                bat 'docker build -t myapp .'
                bat 'docker tag myapp:latest monicas5/myapp'
                bat 'docker push monicas5/myapp:latest'
            }
        }
    }

    post {
        failure {
            // Optional: only include if SMTP is configured
            // mail to: 'you@example.com',
            //      subject: "Build Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
            //      body: "Build failed. Check Jenkins console for details."
        }
    }
}
