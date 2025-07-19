pipeline {
    agent any

    tools {
        maven 'maven-3.9.9'
    }

    triggers {
        githubPush()  // Automatically triggers on GitHub push
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/chandradevops9/Maven2.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                  sh 'mvn sonar:sonar'
            }
        }

        stage('Upload to Artifactory') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                curl -u prakash:LENIN@hitler1 --upload-file target/maven-web-application.war \
                "http://65.1.95.215:8080/manager/text/deploy?path=/maven-web-application&update=true"
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Build and deployment completed successfully"
        }
        failure {
            echo "❌ Build and deployment failed"
        }
        always {
            echo "🔁 Pipeline execution finished"
        }
    }
}

