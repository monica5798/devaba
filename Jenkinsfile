pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9' // Define in Jenkins -> Global Tool Configuration
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
                    def dockerImage = docker.build("monicas5/myapp")
                    docker.withRegistry('', 'docker-hub-credentials') {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            mail to: 'vvce22ise0099@vvce.ac.in',
                 subject: 'Jenkins Build Success: myapp',
                 body: "Build completed successfully!"
        }
        failure {
            mail to: 'vvce22ise0099@vvce.ac.in',
                 subject: 'Jenkins Build Failed: myapp',
                 body: "Build failed. Please check Jenkins logs."
        }
    }
}
