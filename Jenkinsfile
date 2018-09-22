pipeline{

	agent any
	
	parameters {
        string(name: 'jenWorPath', defaultValue: '"C:\\Program Files (x86)\\Jenkins\\workspace\\fullAutomatedPipeline\\webapp\\target\\*.war"', description: 'Who should I say hello to?')

        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
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
					bat 'copy ${params.jenWorPath} C:\\Users\\younes\\projets\\serveurs\\apache-tomcat-8.5.34\\webapps' 
					}
				}
			
				stage('deploy to prod'){
				  steps{
					bat 'copy ${params.jenWorPath} C:\\Users\\younes\\projets\\serveurs\\apache-tomcat-8.5.34second\\webapps'
				  }
				}
			}	
		
		}
	
	
	}


}
