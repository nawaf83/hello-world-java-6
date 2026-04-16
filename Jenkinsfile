pipeline {
agent {
    docker {
        image 'gradle:8.5-jdk17'
    }
}

    environment {// change the below to your jdk path
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-25.0.2+10"
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {

        stage('Verify Environment') {
            steps {
                bat 'echo JAVA_HOME=%JAVA_HOME%'
                bat 'java -version'
            }
        }

        stage('Checkout') { //change the below path to your repositoy url
            steps {
                git branch: 'master', url: 'https://github.com/nawaf83/hello-world-java-6.git'
            }
        }

        stage('Build') {
            steps {
                bat 'gradle clean build --no-daemon'
            }
        }

        stage('Test') {
            steps {
                bat 'gradle test --no-daemon'
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