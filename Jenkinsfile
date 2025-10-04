pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'  // adjust if needed
        MVN_HOME = '/usr/share/maven'                        // adjust if needed
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main', url: 'https://github.com/prasanth-devops/online-bookstore.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project with Maven...'
                sh 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the Spring Boot application...'
                // Run in background, adjust jar name if needed
                sh 'nohup java -jar target/bookstore-0.0.1-SNAPSHOT.jar &'
            }
        }
    }

    post {
        success {
            echo 'Pipeline finished successfully! ✅'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}
