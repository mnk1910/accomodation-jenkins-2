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
                sh 'mvn -f hoteljsf clean install'
            }
        }
        
         // Building the web-service
        stage('Build web-service'){
            steps{
                sh 'mvn -f hotel-restfull clean install'
            }
        }
        
        // Deploy the artifact on glassfish
        stage('Deploy artifacts'){
            steps{
                sh 'asadmin deploy --force=true hotel-restfull/target/hotel-rest.war'
                sh 'asadmin deploy --force=true hoteljsf/target/hotel.war'
            }
        }
        
        // Clean database
        stage('Clean database'){
            steps{
                sh 'psql -h localhost -U postgres hotel -f hoteljsf/database-backup.sql'
            }
        }
        
        // Frontend tests
        stage('Frontend tests'){
            steps{
                sh 'robot -d out-frontend --output output-frontend.xml robotframework-frontend/00_regression_tests.robot'
            }
        }
        
        // Backend tests
        stage('Backend tests'){
            steps{
                sh 'robot -d out-backend --output output-backend.xml robotframework-backend/00_Regression_tests.robot'
            }
        }
        // /Users/monika/.jenkins/workspace/test-jenkins-pipeline/robotframework-frontend/00_regression_tests.robot
    }
        //post actions
        post { 
            always { 
                //Saving the artifacts
				archiveArtifacts '**/**.war'
                
                //Processing the test reports into one
				sh 'rebot -d output --output out.xml out-backend/output-backend.xml out-frontend/output-frontend.xml'
                
				//publishing the robot test results
                step([
				    $class : 'RobotPublisher',
				    outputPath : 'output/',
				    outputFileName : "*.xml",
				    disableArchiveOutput : false,
				    passThreshold : 100,
				    unstableThreshold: 95.0,
				    otherFiles : "*.png",
			    ])
		    }                     	 	
        }

}
