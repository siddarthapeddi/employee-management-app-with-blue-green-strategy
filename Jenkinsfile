pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/siddarthapeddi/employee-management-app-with-blue-green-strategy.git',
                        credentialsId: '5cc29cec-fb86-42dd-840b-d6b76b053f81'
                    ]]
                ])
            }
        }

        stage('Backend Build') {
            steps {
                echo "🔧 Using Maven from Jenkins tool configuration"
                withMaven(maven: 'Maven-3.9.11') {
                    dir('backend') {
                        bat 'mvn -version'
                        bat 'mvn clean package -DskipTests'
                    }
                }
            }
        }

        stage('Frontend Build') {
            steps {
                echo "🌐 Running frontend build"
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

        stage('Docker Build (Optional)') {
            when {
                expression { return false }  // Always skip on Windows
            }
            steps {
                echo "🐳 Docker build skipped on Windows."
            }
        }

        stage('Blue-Green Deployment (Simulated)') {
            steps {
                echo "🔵🟢 Blue-Green deploy skipped (Linux required)."
            }
        }
    }
}
