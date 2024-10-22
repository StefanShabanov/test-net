pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Pulls your code from GitHub
                git branch: 'main', url: 'https://github.com/StefanShabanov/test-net.git'
            }
        }
        stage('Build and Publish') {
            agent {
                docker {
                    // Use the official .NET SDK Docker image
                    image 'mcr.microsoft.com/dotnet/sdk:7.0'
                    reuseNode true
                }
            }
            steps {
                // Navigate to the correct directory and build the project
                dir('SimpleWebApp') {
                    // Publish to a relative directory inside the workspace
                    sh 'dotnet publish -c Release -o ./published_app'
                }
            }
        }
    }
}
