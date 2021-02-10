#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
        VERSION = '0.${currentBuild.number}-SNAPSHOT'
    }
    stages {

	stage('OWASP') {
            steps {
                withGradle {
                    sh './gradlew -PversionNumber=${VERSION} dependencyCheckAnalyze'
                }
            }
            post {
                always {
                    dependencyCheckPublisher pattern: 'build/reports/dependency-check-report.xml'
                }
            }
        }

        stage('QA') {
            steps {
                withGradle {
                    sh './gradlew -PversionNumber=${VERSION} clean check'
                }
                withSonarQubeEnv(credentialsId: 'a821f47c-66dd-4888-859c-90d41bcf26b6', installationName: 'Sonarqube') {
                    sh './gradlew -PversionNumber=${VERSION} sonarqube'
                }
            }
            post {
                always {
                    recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                    recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                }
            }       
        }

        stage('Publish') {
            steps {
                withGradle {
                    withCredentials([string(credentialsId: 'gitlabPrivateToken', variable: 'TOKEN')]) {
                        sh './gradlew -PTOKEN=$TOKEN -PversionNumber=${VERSION} publish'
                    }
                }
            }
        }
    }
}
