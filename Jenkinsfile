pipeline {
    agent any
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
                    sh 'dotnet publish -c Release -o ./published_app'
                }
            }
        }
        stage('Deploy and Run') {
            steps {
                script {
                    // Kill any previous instance of the app running on port 5295
                    sh 'fuser -k 5295/tcp || true'

                    // Run the app in the background and redirect logs for debugging
                    sh '''
                    nohup dotnet /var/lib/jenkins/workspace/test/SimpleWebApp/published_app/SimpleWebApp.dll --urls "http://0.0.0.0:5295" > /var/lib/jenkins/workspace/test/SimpleWebApp/published_app/app.log 2>&1 &
                    '''
                }
            }
        }
    }
}
