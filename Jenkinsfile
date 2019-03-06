/*pipeline{
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
*/
pipeline{
agent { label "master"}
  stages{
    stage('CI'){
      steps{
        script {
			def builders = [:]
			def builders1 = [:]
			File labels1 = new File( "components.txt" )
			def labels = labels1.readLines()
			for ( x in labels ){
				def componentTag = x.split(":")[1].trim()
				println componentTag
				def component = x.split(":")[0].trim()
				println component
				if ( componentTag == "TypeA" ){
                    builders[component] = {
						node {
							stage(component){
								echo component
							}
						}
					}
            } else if ((componentTag == "TypeB") || (componentTag == "TypeC")){
				builders1[component] = {          
					node {
						stage(component){
							echo component
						}
                    }
                }
            }
        }
        if (!builders.isEmpty()){
			parallel builders
         }
         if(!builders1.isEmpty()){
			parallel builders1
         }
        }

      }
    }
  }
}
