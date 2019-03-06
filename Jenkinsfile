pipeline{
	agent {
		label 'master'
	}
	stages{
		stage('Testing'){
			steps{
				script{
					bat 'echo build'
					def deploymentType = readFile 'deployment.txt'
					env.type = deploymentType.split(':')[1].trim()
				}
			}
		}
		stage('deploymentDev'){
			when{
				expression{
					env.type == "DEV" || env.type == "DEV_AND_QA"
				}
			}
			steps{
				echo "Deploying to DEV"
			}
		}
		stage('deploymentQA'){
			when{
				expression{
					env.type == "QA" || env.type == "DEV_AND_QA"
				}
			}
			steps{
				echo "Deploying to QA"
			}
		}
		
	}
}
