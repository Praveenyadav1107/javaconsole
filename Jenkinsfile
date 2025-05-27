opipeline {
    agent any
    tools {
        jdk 'jdk' 
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
    }
}
