def lastSuccessfulCommit = GIT_PREVIOUS_SUCCESSFUL_COMMIT
def currentCommit = GIT_COMMIT

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
				}
		  }
	}
    stage('Build') {
      steps {
        sh 'mvn spring-javaformat:apply'
        sh 'mvn clean'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
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
