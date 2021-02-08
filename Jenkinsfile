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
//                    sh './gradlew clean pmdTest'
                    sh './gradlew clean check'
//                    sh './gradlew spotbugsMain'
//                    sh './gradlew spotbugsTest'
                }
            }
            post {
                always {
//                    archiveArtifacts artifacts: 'build/reports/pitest/mutations.xml'
//                    junit 'build/reports/pitest/mutations.xml'
                    recordIssues (
                        enabledForFailure: true, 
                        tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                    )
                }
            }
        }       
    }
}
