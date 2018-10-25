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
        stage('Build web-service'){
            steps{
                sh 'mvn -f /Users/monika/.jenkins/workspace/test-jenkins-pipeline/hotel-restfull clean install'
            }
        }
        
        // Deploy the artifact on glassfish
        stage('Deploy artifacts'){
            steps{
                sh 'asadmin deploy --force=true /Users/monika/.jenkins/workspace/test-jenkins-pipeline/hotel-restfull/target/hotel-rest.war'
                sh 'asadmin deploy --force=true /Users/monika/.jenkins/workspace/test-jenkins-pipeline/hoteljsf/target/hotel.war'
            }
        }
        
        
    }
}
