#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
	stage('OWASP') {
            steps {
//            withGradle {
//                sh './gradlew dependencyCheckAnalyze'
//            }
                dependencycheck additionalArguments: '--scan ./ --disableYarnAudit --out build/reports/ --format XML', odcInstallation: 'Dependency Checker'
            }
            post {
                always {
                    dependencyCheckPublisher pattern: 'build/reports/*.xml'
                }
            }
        }
/*
        stage('QA') {
            steps {
                withGradle {
                    sh './gradlew clean check'
                }
                withSonarQubeEnv(credentialsId: 'a821f47c-66dd-4888-859c-90d41bcf26b6', installationName: 'Sonarqube') {
                    sh './gradlew sonarqube'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                    recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                }
            }       
        }
*/
    }
}
