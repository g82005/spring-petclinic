pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        // sh 'mvn spring-javaformat:apply'
        // sh 'mvn clean'
		echo 'Build'
      }
    }

    stage('Test') {
      steps {
        // sh 'mvn test'
		echo 'Test'
      }
    }

    stage('Package') {
      steps {
        // sh 'mvn package'
		echo 'Package'
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
    always{
		emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
	}
  }
}
