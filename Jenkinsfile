pipeline {
    agent any

    stages {
        stage('scm') {
            steps {
                git branch: 'main', url: 'https://github.com/naresha/javaconsole'
            }
        }
        stage('build') {
            steps {
                sh './gradlew clean build -x test'
            }
        }
        stage('java') {
            steps {
                sh './gradlew pmdMain'
            }
        }
        stage('checkstyle') {
            steps {
                sh './gradlew checkstyleMain'
            }
        }
    }
}
