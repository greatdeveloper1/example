/*pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
		
		stage('Deploy to staging'){
			steps{
				build job: 'Deploy-to-staging' 
			}
		}
		
		 stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment by me?'
                }

                build job: 'Deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }

    }
}
*/

pipeline{

	agent any
	
	parameters{
			string(name:'ipuat',defaultValue:'localhost',description:'')
			string(name:'ipprod',defaultValue:'localhost',description:'')
	}
	
	triggers{
		pollSCM('* * * * *')
	}
	
	stages{
	
		stage('Compilation et build'){
			
			steps{
				
				echo 'clean and package....'
				bat ' mvn clean package'
			
			}
			post{
			
				success{
					
					echo 'Now archiving the war file ....'
					archiveArtifacts artifacts: '**/*.war'
					
				}
			
			}
		
		}
		
		stage('Deploiment dev et prod'){
		
			parallel{
				
				stage('deploy to UAT'){
				 steps{
					bat " copy **/*.war ${params.ipuat} "
					}
				}
			
				stage('deploy to prod'){
				  steps{
					bat " copy **/*.war ${params.ipprod} "
				  }
				}
			}	
		
		}
	
	
	}


}
