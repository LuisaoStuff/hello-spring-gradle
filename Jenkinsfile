#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'openjdk-15.0.2'
    }
    options {
        ansiColor('xterm')
    }
    stages {
/*
        stage('Build') {
            steps {
                withGradle {
                    sh './gradlew assemble'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'build/libs/*.jar'
                }
            }
        }
*/
        stage('Test') {
            steps {
                withGradle {
//                    sh './gradlew pitest'
                    sh './gradlew clean pmdTest'
                }
            }
            post {
                always {
//                    archiveArtifacts artifacts: 'build/reports/pitest/mutations.xml'
//                    junit 'build/reports/pitest/mutations.xml'
                    recordIssues (
                        enabledForFailure: true, 
                        tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                    )
                }
            }
        }       
    }
}
