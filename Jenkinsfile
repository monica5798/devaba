pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6' // Define in Jenkins -> Global Tool Configuration
        jdk 'JDK 17'         // Same here
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    def dockerImage = docker.build("yourdockerhubusername/myapp")
                    docker.withRegistry('', 'docker-hub-credentials') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: 'Jenkins Build Success: myapp',
                 body: "Build completed successfully!"
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: 'Jenkins Build Failed: myapp',
                 body: "Build failed. Please check Jenkins logs."
        }
    }
}
