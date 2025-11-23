pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    tools {
        maven 'Maven-3.9.11'
        nodejs 'Node-24'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/siddarthapeddi/employee-management-app-with-blue-green-strategy.git',
                        credentialsId: 'github-token'
                    ]]
                ])
                echo "✔ Checkout done"
            }
        }

        stage('Backend Build') {
            steps {
                echo "🔧 Building backend using Maven"
                dir('backend') {
                    bat 'mvn -version'
                    bat 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                echo "🌐 Building frontend"
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
                archiveArtifacts artifacts: 'frontend/dist/**', fingerprint: true
            }
        }

        stage('Blue-Green Deployment (Skipped)') {
            steps {
                echo "🔵🟢 Blue-Green deploy skipped (Windows)"
            }
        }
    }
}
