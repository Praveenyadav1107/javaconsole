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

    post {
        success {
            echo '✅ Build succeeded!'
            archiveArtifacts artifacts: 'build/libs/*.war', fingerprint: true
        }
        failure {
            echo '❌ Build failed! Check console output for details.'
        }
        always {
            junit 'build/test-results/**/*.xml'
            jacoco(
                execPattern: 'build/jacoco/*.exec',
                classPattern: 'build/classes',
                sourcePattern: 'src/main/java'
            )
            recordIssues(
                tools: [
                    checkStyle(pattern: 'build/reports/checkstyle/*.xml'),
                    pmdParser(pattern: 'build/reports/pmd/*.xml')
                ]
            )
            echo '🏁 Build process completed'
        }
    }
}

