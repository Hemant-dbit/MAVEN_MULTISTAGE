pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JDK11'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/<your-username>/maven-multistage-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging artifact...'
                sh 'mvn package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Example placeholder for deploy logic
                sh 'echo "Deploying demo-app.jar to staging environment..."'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
