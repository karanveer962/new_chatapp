pipeline {
    agent {
        label 'slave'
    }
    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonarqube scannerrrrr'
            }
            steps {
                withSonarQubeEnv() {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh "rsync -avhz $WORKSPACE /tmp"
                    sh "ssh jenkins@10.0.0.75 sudo -u chatapp /local/bin/deploy.sh"
                    sh "curl http://54.80.18.121"
                }
            }
        }
    }
}
