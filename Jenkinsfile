pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK18'
    }

    // environment {
    //     GIT_CREDENTIALS_ID = 'autowares-poc'
    //     RECIPIENT_EMAIL = 'kcml@autowares.com'
    // }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Checking out code from Git repository...'
                    git branch: 'main',
                        // credentialsId: "${GIT_CREDENTIALS_ID}",
                        url: 'https://github.com/prasad-moru/petclinic-spring-boot.git'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building Java application with Maven...'
                    sh 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    echo 'Packaging application...'
                    sh 'mvn package'
                }
            }
        }
    }
}
