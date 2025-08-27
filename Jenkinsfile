pipeline {
    agent any

    tools {
        maven 'maven-3.9.11'   // Configure Maven in Jenkins global tools
        jdk 'JAVA_HOME'      // Configure JDK in Jenkins global tools
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/thulasiv199/simple-javaapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application (simulation)..."
                // Example: Copy jar to a server
                sh 'scp target/simple-java-app-1.0-SNAPSHOT.jar ubuntu@172.31.40.227:/opt/apps/'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
