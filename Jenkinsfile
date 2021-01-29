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
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'
                }
            }
        }       
    }
}
