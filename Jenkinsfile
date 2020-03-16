def currentCommit = env.GIT_COMMIT
def previousSucess = readFile 'PreviousSucess.txt'
def count = readFile 'Count.txt'
pipeline {
  agent any
  stages {
		stage('Phase 1') {
			steps {
				script{
					echo "${count.trim()}"
					echo "${previousSucess}.trim()"
					
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

