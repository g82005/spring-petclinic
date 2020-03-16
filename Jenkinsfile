def lastSuccessfulCommit = $env.GIT_PREVIOUS_SUCCESSFUL_COMMIT
def currentCommit = $env.GIT_COMMIT
def previousSucess = readFile 'PreviousSucess.txt'
def count = readFile 'Count.txt'
pipeline {
  agent any
  stages {
		stage('Phase 1') {
			steps {
					echo "${count.trim()}"
					echo "${previousSucess}.trim()"
					if(${previousSucess}.trim()){
						echo 'No previous sucess build, going to build.'
					}
					else{
						if(${count.trim()}.toInteger()>=8){
							echo 'Having 8 commits, going to build.'
						}
						else{
							newCount = ${count.trim()}.toInteger() + 1
							sh 'echo ${newCount} > Count.txt'
							echo 'increment count to ${count.trim().toInteger(). Exiting.}'
							exit 0
						}
					}
				}
			}
		
		stage('Build') {
		  steps {
			echo 'Building'
			// sh 'mvn spring-javaformat:apply'
			// sh 'mvn clean'
		  }
		}

		stage('Test') {
		  steps {
					echo 'Testing..'
					// sh 'mvn test'
					
					if(${currentBuild.result}.equals("FAILURE")){
						
					}
				}
		}
		stage('Package') {
		  steps {
			echo 'Packaging'
			// sh 'mvn package'
		  }
		}

		
		
	}
	post {
    	failure {
			echo 'Testing failed!'
			if(${previousSucess.}trim()!=NULL){				
				sh "git bisect start $env.GIT_COMMIT ${previousSucess}.trim()"
				sh "git bisect run mvn clean test"
				sh "git bisect reset"
			}			
    	}
   }

}

