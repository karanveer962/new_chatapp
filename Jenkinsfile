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
                withSonarQubeEnv('SonarQubeServer') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh "rsync -avz $WORKSPACE jenkins@10.0.0.75:/tmp/"
                    sh 'ssh jenkins@10.0.0.75 "sudo -u chatapp /usr/local/bin/deploy.sh"'
                }
            }
        }
    }
}
