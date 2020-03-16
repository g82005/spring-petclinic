def currentCommit = env.GIT_COMMIT
def count = readFile 'Count.txt'
pipeline {
  agent any
  stages {
		stage('Phase 1') {
			steps {
				script{
					count = readFile 'Count.txt'
					echo "${count.trim()}"
					echo "${previousSucess}.trim()"
					if(${previousSucess}.trim()){
						echo 'No previous sucess build, going to build.'
					}
					else{
						if(${count.trim()}.toInteger()>=8){
							echo 'Having 8 commits, going to build.'
							sh 'echo "0" > Count.txt'
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
			script{
				if(${previousSucess}.trim()!=NULL){				
				sh "git bisect start $GIT_COMMIT ${previousSucess}.trim()"
				sh "git bisect run mvn clean test"
				sh "git bisect reset"
				}
			}	
    	}
   }

}

