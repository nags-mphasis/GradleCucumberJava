pipeline {

    agent any

    stages {
        stage('build') {
            steps {
                sh './gradlew clean'
            }
        }
        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test -Dcucumber.options="/src/test/resources/Features/Smoke.feature"'
            }
        }
        stage('Test Reports') {
            steps {
                cucumber buildStatus: 'UNSTABLE',
                reportTitle: 'Smoke Test',
                fileIncludePattern: '**/*.json'
                /*
                publishHTML (target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'target/SmokeReports',
                reportFiles: 'Reports.json',
                reportName: "Cucumber Report"
                ])
                */
            }
        }
    }
    
    post {
        unsuccessful {
            cleanWs()
        }
    }
}
