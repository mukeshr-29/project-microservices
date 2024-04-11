pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('sonarqube analysis'){
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token', installationName: 'sonar-server') {
                        sh '''
                            $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=shippingservice -Dsonar.projectName=shippingservice -Dsonar.java.binaries=. 
                        '''
                    }
                }
            }
        }
        stage('quality gate'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                        sh "docker build -t mukeshr29/shippingservice1:latest ."
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                        sh "docker push mukeshr29/shippingservice1:latest "
                    }
                }
            }
        }
    }
}
