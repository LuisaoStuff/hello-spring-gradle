#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'openjdk-11'
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
        }
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test'
                }
            }
        }
    }
}
