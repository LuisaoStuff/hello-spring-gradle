#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
                configFileProvider([configFile(fileId: 'gradle-properties-sonarqube', targetLocation: 'gradle.properties')]) {
                    withGradle {
                        sh './gradlew sonarqube'
                        sh './gradlew clean check'
                    }
                }

            }
/*
            post {
                always {
                    archiveArtifacts artifacts: 'build/reports/pitest/mutations.xml'
                    junit 'build/reports/pitest/mutations.xml'
                    recordIssues (
                        enabledForFailure: true, 
                        tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                    )
                    recordIssues (
                        enabledForFailure: true, 
                        tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                    )

                }
            }
*/



        }       
    }
}
