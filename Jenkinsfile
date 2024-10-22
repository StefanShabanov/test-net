pipeline {
    agent any
    environment {
        DOTNET_CLI_HOME = "${env.WORKSPACE}/.dotnet"
        HOME = "${env.WORKSPACE}"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/StefanShabanov/test-net.git'
            }
        }
        stage('Build and Publish') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:8.0'
                    reuseNode true
                }
            }
            steps {
                dir('SimpleWebApp') {
                    // Set environment variables and run dotnet publish
                    sh 'dotnet publish -c Release -o ./published_app'
                }
            }
        }
    }
}
