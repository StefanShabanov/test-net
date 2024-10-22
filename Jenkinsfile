pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Pulls your code from GitHub
                git branch: 'main', url: 'https://github.com/StefanShabanov/test-net/tree/main/SimpleWebApp'
            }
        }
        stage('Build and Publish') {
            agent {
                docker {
                    // Use the official .NET SDK Docker image
                    image 'mcr.microsoft.com/dotnet/sdk:7.0'
                }
            }
            steps {
                // Build and publish the app
                sh 'dotnet publish -c Release -o /var/jenkins_home/published_app'
            }
        }
    }
}
