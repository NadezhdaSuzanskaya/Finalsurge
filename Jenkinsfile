pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {
        stage('tests') {
            steps {
                git branch: '$BRANCH', url: 'https://github.com/NadezhdaSuzanskaya/Finalsurge.git'

                sh "mvn clean test -Dmaven.test.failure.ignore=true -Dmaven.compiler.source=11 -Dmaven.compiler.target=11"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('reports') {
            steps {
                script {
                    allure([
                            includeProperties: false,
                            jdk: '',
                            properties: [],
                            reportBuildPolicy: 'ALWAYS',
                            results: [[path: 'target/allure-results']]
                    ])
                }
            }
        }
    }
}