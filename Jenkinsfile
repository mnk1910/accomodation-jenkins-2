pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        
        // Building the web-app
        stage('Build web-app'){
            steps{
                sh 'mvn -f /Users/monika/.jenkins/workspace/test-jenkins-pipeline/hoteljsf clean install'
            }
        }
        
         // Building the web-service
        stage('Build web-app'){
            steps{
                sh 'mvn -f /Users/monika/.jenkins/workspace/test-jenkins-pipeline/hotel-restfull clean install'
            }
        }
    }
}
