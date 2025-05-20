pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
        jdk 'JDK 17'
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
            mail to: 'vvce22ise0099@vvce.ac.in',
                 subject: "Build Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                 body: "Build failed. Check Jenkins console for details."
        }
    }
}
