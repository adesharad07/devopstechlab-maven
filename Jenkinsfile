pipeline {
    agent any
    tools{
        maven 'maven3.9'
        jdk 'jdk17'
    }

    stages {
        stage('Git-Download') {
            steps {
                git branch: 'main', url: 'https://github.com/adesharad07/devopstechlab-maven.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
            }
        }
        stage('Archieve-Artifact') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('build-nextjob') {
            steps {
                timeout(time: 30, unit: 'SECONDS') {
                    input 'Do you want to proceed?'
                }
                build 'deploy-to-prod'
            }
        }
    }
}
