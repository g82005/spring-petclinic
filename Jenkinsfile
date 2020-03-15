def lastSuccessfulCommit = env.GIT_PREVIOUS_SUCCESSFUL_COMMIT
def currentCommit = env.GIT_COMMIT

pipeline {
  agent any
  stages {
	stage('Phase 1') {
		steps {
			script {
				  if (lastSuccessfulCommit) {
					commits = sh(
					  script: "git rev-list $currentCommit \"^$lastSuccessfulCommit\"",
					  returnStdout: true
					).split('\n')			
					echo 'Commits are: $commits'
					}
				else{
					echo 'No lastSuccessfulCommit'
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
		echo 'Testing'
        // sh 'mvn test'
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
}
