pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-1.8"
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {

        stage('Verify Environment') {
            steps {
                bat 'echo JAVA_HOME=%JAVA_HOME%'
                bat 'java -version'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/nawaf83/hello-world-java-6.git'
            }
        }

        stage('Fix Gradle Wrapper Permission') {
            steps {
                // Ensure gradlew works on all machines
                bat 'if exist gradlew.bat (echo Gradle wrapper exists)'
            }
        }

        stage('Build') {
            steps {
                bat 'gradlew.bat clean build --no-daemon'
            }
        }

        stage('Test') {
            steps {
                bat 'gradlew.bat test --no-daemon'
            }
        }


        stage('Deploy') {
            steps {
                bat 'java -jar build\\libs\\hello-world-java-V1.0.jar'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir()
        }
        success {
            echo 'Build succeeded!!!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}