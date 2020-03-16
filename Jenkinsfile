def previousSucess
def count

pipeline {
  agent any
  stages {
	stage('Phase 1') {
		steps {
			script {
				  count = readFile("D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/Count.txt").trim().toInteger()
				  previousSucess = readFile("D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/PreviousSucess.txt").trim()
				  echo "${count}"
				  echo "${previousSucess}"
				  echo "$env.GIT_COMMIT"
				  cc = $env.GIT_COMMIT"
				  echo "${cc}"
					if( previousSucess == "" ){
						echo 'No previous sucess build, going to build.'
					}
					else{
						if( count >=8 ){
							echo "${count}"
							echo 'Having 8 commits, going to build.'
							sh 'echo "0" > Count.txt'
						}
						else{
							newCount = ${count} + 1
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
		sh 'echo "$env.GIT_COMMIT" > "D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/PreviousSucess.txt"'
      }
    }

    stage('Package') {
      steps {
	    echo 'Packaging'
        // sh 'mvn package'
      }
    }

    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Deploying'
      }
    }

  }
  post {
    	failure {
			echo 'Testing failed!'
			script{
				if ( previousSucess != NULL) {				
				sh "git bisect start $GIT_COMMIT ${previousSucess}"
				sh "git bisect run mvn clean test"
				sh "git bisect reset"
				}
			}	
    	}
   }
}
