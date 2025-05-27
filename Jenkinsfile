pipeline {
    agent any

    stages {
        stage('scm') {
            steps {
                git branch: 'main', url: 'https://github.com/naresha/javaconsole'
            }
        stage('build') {
            steps {
                sh 'gradle build'
            }
        }
    }
}
