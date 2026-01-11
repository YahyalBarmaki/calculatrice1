pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
        jdk 'JDK-17'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Récupération du code source...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilation du projet...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Exécution des tests unitaires...'
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Création du JAR...'
                sh 'mvn package -DskipTests'
            }
        }

        /*
        stage('Build Docker Image') {
            steps {
                echo 'Construction de l\'image Docker...'
                sh 'docker build -t calculatrice:${BUILD_NUMBER} .'
                sh 'docker tag calculatrice:${BUILD_NUMBER} calculatrice:latest'
            }
        }
        */
    }

    post {
        success {
            echo 'Pipeline exécuté avec succès !'
        }
        failure {
            echo 'Le pipeline a échoué.'
        }
        always {
            echo 'Nettoyage...'
            cleanWs()
        }
    }
}