pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                checkout scm
            }
        }
        
        // Building the web app
        stage('Build web-app'){
            steps{
                sh 'echo hello world2!'
            }
        }
    }
}
