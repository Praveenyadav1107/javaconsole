pipeline {
    agent any
    tools {
        jdk 'jdk'  // Requires JDK tool configuration in Jenkins
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
    }
    stages {
        stage('scm') {
            steps {
                git branch: 'main', url: 'https://github.com/naresha/demoweb'
            }
        }
        stage('build') {
            steps {
                sh './gradlew clean build -x test'
            }
        } 
        stage('jdk') {
            steps {
                sh './gradlew pmdMain'
            }
        } 
        stage('code conventions') {
            steps {
                sh './gradlew checkstyleMain'
            }
        } 
        stage('automated test') {
            steps {
                sh './gradlew test jacocoTestReport'
            }
        }
    }
}
